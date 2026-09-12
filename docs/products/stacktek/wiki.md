# StackTek Wiki

StackTek is a self-hosted workspace platform you run on your own server. It launches fully isolated web desktops, AI agents, and Linux apps as disposable containers and serves them straight to your browser over TLS — no VPN, no SSH, no client software. Everything is fronted by a Caddy + OWASP CRS web application firewall and runs on rootless Podman.

!!! warning "Active Development"

    StackTek is in active development and is **not fully functional** yet. Expect missing features, rough edges, and breaking changes between versions.

- **Privacy:** See the [StackTek Privacy Policy](/products/stacktek/privacy/)
- **Product page:** [decyphertek.io/products/stacktek](https://decyphertek.io/products/stacktek/)
- **License:** PolyForm Noncommercial — free for personal use, tinkering, research, and education

## Features

- **Web Desktops** — Full Linux desktops (Arch, Debian, Ubuntu, Fedora, Kali, Rocky, and more) with XFCE, GNOME, or KDE, rendered in the browser via VNC
- **AI Agents** — LibreChat, Open WebUI, Flowise, Agent Zero, and other agent stacks, each in its own container
- **Apps** — Chromium, LibreOffice, VSCodium, Thunderbird, and more
- **CyberLab** — Deliberately vulnerable apps (DVWA, WebGoat, Mutillidae) for security training

Each launch builds a fresh, isolated container on a private network. Nothing persists unless you set it to. Workspaces are torn down on stop; session data lives in `~/stacktek/data` on the host.

## Requirements

- A Linux server with [rootless Podman](https://docs.podman.io/en/latest/markdown/podman.1.html) and `podman-compose`
- Port 443 free
- Your user's Podman socket enabled (`systemctl --user enable --now podman.socket`)
- The compose file assumes your user is UID 1000 (the first user on most distros) — adjust the socket path in `compose.yml` if yours differs
- Tested with Podman only; Docker Compose is not officially supported

## Getting Started

1. Create the directory layout and TLS certs (self-signed is fine for self-hosting):

```bash
mkdir -p ~/stacktek/certs ~/stacktek/caddy
openssl req -x509 -newkey ec -pkeyopt ec_paramgen_curve:prime256v1 \
  -keyout ~/stacktek/certs/key.pem -out ~/stacktek/certs/cert.pem \
  -days 3650 -nodes -subj "/O=decyphertek/CN=stacktek"
```

2. Save this as `~/stacktek/caddy/Caddyfile` (the Caddy edge config with the WAF):

```
{
    # Self-signed certs — no public CA issuance.
    auto_https off

    # Coraza WAF runs before the proxy so it can short-circuit
    # malicious requests before they hit the upstream.
    order coraza_waf before reverse_proxy
}

:443 {
    tls /certs/cert.pem /certs/key.pem

    encode zstd gzip

    # WebSocket paths bypass Coraza — Coraza wraps ResponseWriter and removes
    # http.Hijacker, which Caddy's reverse_proxy requires for protocol upgrades.
    @websocket path /ws/*
    handle @websocket {
        reverse_proxy https://stacktek:8443 {
            header_up X-Forwarded-Proto https
            header_up X-Forwarded-For   {remote_host}
            header_up X-Real-IP         {remote_host}
            transport http {
                tls
                tls_insecure_skip_verify
            }
        }
    }

    # All other requests go through the Coraza WAF — OWASP Core Rule Set.
    handle {
        coraza_waf {
            load_owasp_crs
            directives `
                Include @coraza.conf-recommended
                Include @crs-setup.conf.example
                Include @owasp_crs/*.conf
                SecRuleEngine On
                SecRequestBodyAccess On
                SecResponseBodyAccess Off
            `
        }

        reverse_proxy https://stacktek:8443 {
            header_up X-Forwarded-Proto https
            header_up X-Forwarded-For   {remote_host}
            header_up X-Real-IP         {remote_host}
            transport http {
                tls
                tls_insecure_skip_verify
            }
        }
    }

    # Hardening response headers. X-Frame-Options is SAMEORIGIN (not DENY)
    # because the stacktek SPA iframes /ws/vnc/* and /apps/* on its own
    # origin to render desktops and web apps inline.
    header {
        Strict-Transport-Security "max-age=31536000"
        X-Content-Type-Options    "nosniff"
        X-Frame-Options           "SAMEORIGIN"
        Referrer-Policy           "no-referrer"
        -Server
    }

    log {
        output stdout
        format console
        level DEBUG
    }
}
```

3. Save this as `~/stacktek/compose.yml` and run it:

```yaml
networks:
  stacktek:
    driver: bridge

services:
  stacktek:
    image: ghcr.io/decyphertek-io/stacktek/stacktek:latest
    container_name: stacktek
    networks: [stacktek]
    expose:
      - "8443"
    environment:
      - RUST_LOG=stacktek=debug,stacktek::proxy=debug,tower_http=info
      - STACKTEK_BIND=0.0.0.0:8443
      - STACKTEK_WORKSPACES=/workspaces
      - STACKTEK_DATA=/data
      - STACKTEK_DATA_HOST_DIR=$HOME/stacktek/data
      - STACKTEK_STATIC=/static
      - STACKTEK_TLS_CERT=/certs/cert.pem
      - STACKTEK_TLS_KEY=/certs/key.pem
    volumes:
      - $HOME/stacktek/data:/data:rw
      - $HOME/stacktek/certs:/certs:ro,z
      - /run/user/1000/podman/podman.sock:/run/podman.sock:z
    security_opt:
      - "label:disable"
    restart: unless-stopped
    healthcheck:
      test: ["CMD", "/stacktek", "healthcheck"]
      interval: 30s
      timeout: 5s
      retries: 3
      start_period: 20s

  caddy:
    image: ghcr.io/decyphertek-io/stacktek/caddy-coraza:latest
    container_name: stacktek-caddy
    depends_on:
      stacktek:
        condition: service_healthy
    networks: [stacktek]
    ports:
      - "443:443"
    volumes:
      - $HOME/stacktek/caddy/Caddyfile:/etc/caddy/Caddyfile:ro,z
      - $HOME/stacktek/certs:/certs:ro,z
      - $HOME/stacktek/caddy/data:/data:rw,Z
      - $HOME/stacktek/caddy/config:/config:rw,Z
    restart: unless-stopped
    healthcheck:
      test: ["CMD-SHELL", "wget -qO- --no-check-certificate https://127.0.0.1/api/health >/dev/null || exit 1"]
      interval: 30s
      timeout: 5s
      retries: 3
```

4. Start it:

```bash
cd ~/stacktek
podman-compose up -d
```

5. Open `https://<your-server-ip>/` and accept the self-signed certificate warning.

Images are pulled automatically from GHCR — the workspace catalog is baked into the stacktek image, so there is nothing else to download or clone.

## Manage It

```bash
# Update to the latest images (also refreshes the workspace catalog)
podman-compose pull
podman-compose up -d

# Stop
podman-compose down

# Logs
podman logs stacktek
podman logs stacktek-caddy
```

## Support

- [GitHub Issues](https://github.com/decyphertek-io/stacktek)
- [Website](https://decyphertek.io/)
