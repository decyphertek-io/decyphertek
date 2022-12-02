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
        ssl_ciphers          HIGH:!aNULL:!MD5;
        ssl_prefer_server_ciphers on;
    location / {
        proxy_pass http://localhost:8080;
        proxy_ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection upgrade;
        proxy_set_header Accept-Encoding gzip;
        }
    }
    $ sudo nginx -t
    $ sudo systemctl daemon-reload
    $ sudo systemctl start nginx

Optional: ModSecurity 
-----------

    $ sudo apt update && sudo apt install -y git gcc make build-essential autoconf automake libtool libcurl4-openssl-dev liblua5.3-dev libfuzzy-dev ssdeep gettext pkg-config libpcre3 libpcre3-dev libxml2 libxml2-dev libcurl4 libgeoip-dev libyajl-dev doxygen libpcre++-dev libpcre2-16-0 libpcre2-dev libpcre2-posix3 
    $ sudo mkdir /usr/local/src/nginx && cd /usr/local/src/nginx
    # May have to run twice if you get an error. 
    $ sudo su -c "apt source nginx"
    $ ls 
    $ nginx -v
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
    $ sudo apt build-dep nginx -y && sudo apt install -y uuid-dev
    $ sudo ./configure --with-compat --add-dynamic-module=/usr/local/src/ModSecurity-nginx
    $ sudo make modules
    $ sudo cp /usr/local/src/nginx/nginx-1.22.1/objs/ngx_http_modsecurity_module.so /etc/nginx/modules/
    $ sudo vim /etc/nginx/nginx.conf
    load_module modules/ngx_http_modsecurity_module.so;
    events {
        worker_connections  1024;
    }

    http {
        modsecurity on;
        modsecurity_rules_file /etc/nginx/modsec/modsec-config.conf;
        include       /etc/nginx/mime.types;
    $ sudo mkdir /etc/nginx/modsec/
    $ sudo cp /usr/local/src/ModSecurity/modsecurity.conf-recommended /etc/nginx/modsec/modsecurity.conf
    $ sudo vim /etc/nginx/modsec/modsecurity.conf
    # Change SecRuleEngine DetectionOnly 
    SecRuleEngine On
    # Change SecAuditLogParts ABIJDEFHZ
    SecAuditLogParts ABCEFHJKZ
    $ sudo vim /etc/nginx/modsec/modsec-config.conf
    Include /etc/nginx/modsec/modsecurity.conf
    $ sudo cp /usr/local/src/ModSecurity/unicode.mapping /etc/nginx/modsec/
    $ sudo nginx -t
    $ sudo systemctl restart nginx
    $ cd /etc/nginx/modsec
    $ sudo su -c "wget https://github.com/coreruleset/coreruleset/archive/refs/tags/v3.3.2.zip"
    $ sudo apt install unzip -y
    $ sudo unzip v3.3.2.zip 
    $ sudo cp /etc/nginx/modsec/coreruleset-3.3.2/crs-setup.conf.example /etc/nginx/modsec/coreruleset-3.3.2/crs-setup.conf
    $ sudo vim /etc/nginx/modsec/modsec-config.conf
    Include /etc/nginx/modsec/coreruleset-3.3.2/crs-setup.conf
    Include /etc/nginx/modsec/coreruleset-3.3.2/rules/*.conf
    $ sudo nginx -t
    $ sudo systemctl restart nginx
    $ sudo vim /etc/nginx/modsec/coreruleset-3.3.2/crs-setup.conf
    # No need to change these are the defaults. 
    Anomaly Scoring Mode 
    Paranoia Level 1 
    $ sudo vim /etc/logrotate.d/modsec
    /var/log/modsec_audit.log
    {
        rotate 31
        daily
        missingok
        compress
        delaycompress
        notifempty
    }
    # Test - should get 403 forbidden
    $ sudo tail -f /var/log/modsec_audit.log
    # Open up a web browser and test to see if the log shows up. 
    $ https://www.yourdomain.com/index.html?exec=/bin/bash
    # Whitelisting an errors regarding legitmate traffic
    # Id eqauls unique_id = first twelve numbers , 
    # using id produces error and the full unique id produces an error
    # adding multiple ips to @ipmatch also procues an error. 
    $ sudo cp /etc/nginx/modsec/coreruleset-3.3.2/rules/REQUEST-900-EXCLUSION-RULES-BEFORE-CRS.conf.example /etc/nginx/modsec/coreruleset-3.3.2/rules/REQUEST-900-EXCLUSION-RULES-BEFORE-CRS.conf
    $ sudo vim /etc/nginx/modsec/coreruleset-3.3.2/rules/REQUEST-900-EXCLUSION-RULES-BEFORE-CRS.conf
    SecRule REMOTE_ADDR "^195\.151\.128\.96" "id:987987987987,phase:1,nolog,allow,ctl:ruleEngine=off"
    ## or ###
    SecRule REMOTE_ADDR "@ipMatch 195.151.128.96" "phase:1,id:987987987987,allow,ctl:ruleEngine=off"
    # Find additonal rules to add
    $ sudo cat /var/log/modsec_audit.log | grep unique_id
    # I also found a way to disable the rule entirely , example - this rule blocks odoo webstire builder , can re-eanble when site built. 
    $ cd /etc/nginx/modsec/coreruleset-3.3.2/rules
    $ sudo mv REQUEST-941-APPLICATION-ATTACK-XSS.conf REQUEST-941-APPLICATION-ATTACK-XSS.conf.disable
    $ sudo mv REQUEST-949-BLOCKING-EVALUATION.conf REQUEST-949-BLOCKING-EVALUATION.conf.disable
    
References
----------

    https://www.nginx.com/resources/wiki/start/topics/tutorials/install/
    https://www.ibm.com/support/pages/how-configure-nginx-ssl-reverse-proxy
    https://www.linuxcapable.com/how-to-install-nginx-with-modsecurity-3-on-ubuntu-22-04-lts/
    