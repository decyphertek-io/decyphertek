Nginx
=====

Nginx reverse proxy can be used to encrypt web traffic. 

Install
-------

    $ sudo vim /etc/apt/sources.list.d/nginx.list
    deb https://nginx.org/packages/ubuntu/ jammy nginx
    deb-src https://nginx.org/packages/ubuntu/ jammy nginx
    $ sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys ABF5BD827BD9BF62
    $ sudo apt update && sudo apt -y install nginx 
    ### Optional: Modsec ####
    $ sudo mkdir /usr/local/src/nginx && cd /usr/local/src/nginx
    $ sudo su -c "apt source nginx"
    $ ls 
    $ nginx -v
    ### Optional: Modesc - End ###
    $ sudo systemctl enable nginx
    $ sudo unlink /etc/nginx/conf.d/default.conf
    $ sudo openssl req -x509 -nodes -days 1095 -newkey rsa:2048 -keyout /etc/ssl/private/self-signed-key.pem -out /etc/ssl/certs/self-signed-crt.pem -subj "/C=US/ST=Any/L=Anytown/O=decyphertek-io/OU=adminotaur/CN=decyphertek"
    $ sudo vim /etc/nginx/conf.d/custom.conf
    server {
        listen 443 ssl;
        server_name localhost;
        ssl_certificate      /etc/ssl/certs/self-signed-crt.pem;
        ssl_certificate_key  /etc/ssl/private/self-signed-key.pem;
        ssl_session_cache    shared:SSL:1m;
        ssl_session_timeout  5m;
        ssl_protocols        TLSV1.1 TLSV1.2 TLSV1.3;
        ssl_ciphers  HIGH:!aNULL:!MD5;
        ssl_prefer_server_ciphers  on;
    location / {
        proxy_pass http://localhost:63443;
        proxy_ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
        }
    }
    $ sudo nginx -t
    $ sudo systemctl daemon-reload
    $ sudo systemctl start nginx

Optional: ModSecurity 
-----------

    $ sudo apt update && sudo apt install -y git gcc make build-essential autoconf automake libtool libcurl4-openssl-dev liblua5.3-dev libfuzzy-dev ssdeep gettext pkg-config libpcre3 libpcre3-dev libxml2 libxml2-dev libcurl4 libgeoip-dev libyajl-dev doxygen libpcre++-dev libpcre2-16-0 libpcre2-dev libpcre2-posix3 
    $ sudo git clone --depth 1 -b v3/master --single-branch https://github.com/SpiderLabs/ModSecurity /usr/local/src/ModSecurity/
    $ cd /usr/local/src/ModSecurity/
    $ sudo git submodule init
    $ sudo git submodule update
    $ sudo ./build.sh
    $ sudo ./configure
    $ sudo make
    $ sudo make install
    $ sudo git clone --depth 1 https://github.com/SpiderLabs/ModSecurity-nginx.git /usr/local/src/ModSecurity-nginx/
    $ cd /usr/local/src/nginx/nginx-1.*.*
    $ sudo apt build-dep nginx && sudo apt install uuid-dev
    $ sudo ./configure --with-compat --add-dynamic-module=/usr/local/src/ModSecurity-nginx
    $ sudo make modules
    $ sudo cp objs/ngx_http_modsecurity_module.so /usr/share/nginx/modules/
    $ sudo nano /etc/nginx/nginx.conf
    load_module modules/ngx_http_modsecurity_module.so;
    http{
    modsecurity on;
    modsecurity_rules_file /etc/nginx/modsec/modsec-config.conf;
    $ sudo mkdir /etc/nginx/modsec/
    $ sudo cp /usr/local/src/ModSecurity/modsecurity.conf-recommended /etc/nginx/modsec/modsecurity.conf
    $ sudo nano /etc/nginx/modsec/modsecurity.conf
    # Change SecRuleEngine DetectionOnly 
    SecRuleEngine On
    # Change SecAuditLogParts ABIJDEFHZ
    SecAuditLogParts ABCEFHJKZ
    $ sudo nano /etc/nginx/modsec/modsec-config.conf
    Include /etc/nginx/modsec/modsecurity.conf
    $ sudo cp /usr/local/src/ModSecurity/unicode.mapping /etc/nginx/modsec/
    $ sudo nginx -t
    $ sudo systemctl restart nginx
    $ cd /etc/nginx/modsec
    $ wget https://github.com/coreruleset/coreruleset/archive/refs/tags/v3.3.2.zip
    $ sudo apt install unzip -y
    $ sudo unzip v3.3.2.zip -d /etc/nginx/modsec
    $ sudo cp /etc/nginx/modsec/coreruleset-3.3.2/crs-setup.conf.example /etc/nginx/modsec/coreruleset-3.3.2/crs-setup.conf
    $ sudo nano /etc/nginx/modsec/modsec-config.conf
    Include /etc/nginx/modsec/coreruleset-3.3.2/crs-setup.conf
    Include /etc/nginx/modsec/coreruleset-3.3.2/rules/*.conf
    $ sudo nginx -t
    $ sudo systemctl restart nginx
    $ sudo nano /etc/nginx/modsec/coreruleset-3.3.2/crs-setup.conf
    Anomaly Scoring Mode 
    Paranoia Level 1 
    # Test - should get forbidden
    $ https://www.yourdomain.com/index.html?exec=/bin/bash
    # Read Reference regarding false postives and whitelisting
    $ sudo nano /etc/logrotate.d/modsec

References
----------

    https://phoenixnap.com/kb/nginx-reverse-proxy
    https://www.ibm.com/support/pages/how-configure-nginx-ssl-reverse-proxy
    https://www.linuxcapable.com/how-to-install-nginx-with-modsecurity-3-on-ubuntu-22-04-lts/
    