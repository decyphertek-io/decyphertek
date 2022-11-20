Nginx
=====

Nginx reverse proxy can be used to encrypt web traffic. 

Install
--------

    $ sudo apt -y install nginx
    $ sudo systemctl enable nginx
    $ sudo unlink /etc/nginx/sites-enabled/default
    $ sudo openssl req -x509 -nodes -days 1095 -newkey rsa:2048 -keyout /etc/ssl/private/self-signed-key.pem -out /etc/ssl/certs/self-signed-crt.pem -subj "/C=US/ST=Any/L=Anytown/O=decyphertek-io/OU=adminotaur/CN=decyphertek"
    $ sudo vim /etc/nginx/sites-enabled/custom-ssl.conf
    server {
        listen       443 ssl;
        ssl_certificate      /etc/ssl/certs/self-signed-crt.pem;
        ssl_certificate_key  /etc/ssl/private/self-signed-key.pem;
        ssl_session_cache    shared:SSL:1m;
        ssl_session_timeout  5m;
        ssl_protocols        TLSV1.1 TLSV1.2 TLSV1.3;

        ssl_ciphers  HIGH:!aNULL:!MD5;
        ssl_prefer_server_ciphers  on;

    location / {
        proxy_pass https://localhost:63443;
        proxy_ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
    }
    $ sudo systemctl daemon-reload
    $ sudo systemctl start nginx

References
----------

    https://phoenixnap.com/kb/nginx-reverse-proxy
    https://www.ibm.com/support/pages/how-configure-nginx-ssl-reverse-proxy
    