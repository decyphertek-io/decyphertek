Mastadon
=========

Self hosted decentralize open source social media alternative.

Install Requirements
---------------------

    $ sudo su
    $ apt install -y curl wget gnupg apt-transport-https lsb-release ca-certificates 
    $ curl -fsSL https://deb.nodesource.com/gpgkey/nodesource.gpg.key | apt-key add -
    $ curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash - 
    $ wget -O /usr/share/keyrings/postgresql.asc https://www.postgresql.org/media/keys/ACCC4CF8.asc echo "deb [signed-by=/usr/share/keyrings/postgresql.asc] http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/postgresql.list 
    $ apt update && apt install -y imagemagick ffmpeg libpq-dev libxml2-dev libxslt1-dev file git-core g++ libprotobuf-dev protobuf-compiler pkg-config nodejs gcc autoconf bison build-essential libssl-dev libyaml-dev libreadline6-dev zlib1g-dev libncurses5-dev libffi-dev libgdbm-dev nginx redis-server redis-tools postgresql postgresql-contrib certbot python3-certbot-nginx libidn11-dev libicu-dev libjemalloc-dev 
    $ corepack enable 
    $ yarn set version stable 

Installing Ruby
---------------

    $ adduser --disabled-login mastodon
    $ su - mastodon
    $ git clone https://github.com/rbenv/rbenv.git ~/.rbenv
    $ cd ~/.rbenv && src/configure && make -C src
    $ echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
    $ echo 'eval "$(rbenv init -)"' >> ~/.bashrc
    $ exec bash
    $ git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build
    $ RUBY_CONFIGURE_OPTS=--with-jemalloc rbenv install 3.0.3
    $ rbenv global 3.0.3
    $ gem install bundler --no-document
    $ exit

PostGresSQL
-----------

    # Optional hardware config tuning: https://pgtune.leopard.in.ua/#/  - Generates config /etc/postgresql/14/main/postgresql.conf . 
    $ sudo -u postgres psql
    $ CREATE USER mastodon CREATEDB;
    $ \q

Mastadon Setup
--------------

    $ su - mastodon
    $ git clone https://github.com/tootsuite/mastodon.git live && cd live
    $ git checkout $(git tag -l | grep -v 'rc[0-9]*$' | sort -V | tail -n 1)
    $ bundle config deployment 'true'
    $ bundle config without 'development test'
    $ bundle install -j$(getconf _NPROCESSORS_ONLN)
    $ yarn install --pure-lockfile
    # Need to set a domain name and unable to change.
    $ RAILS_ENV=production bundle exec rake mastodon:setup
    # config stored .env.production
    # Example
    mastodon@decyphertek:~/live$ RAILS_ENV=production bundle exec rake mastodon:setup
    Your instance is identified by its domain name. Changing it afterward will break things.
    Domain name: 127.0.0.1

    Single user mode disables registrations and redirects the landing page to your public profile.
    Do you want to enable single user mode? No

    Are you using Docker to run Mastodon? no

    PostgreSQL host: /var/run/postgresql
    PostgreSQL port: 5432
    Name of PostgreSQL database: mastodon_production
    Name of PostgreSQL user: mastodon
    Password of PostgreSQL user: 
    Database configuration works! 🎆

    Redis host: localhost
    Redis port: 6379
    Redis password: 
    Redis configuration works! 🎆

    Do you want to store uploaded files on the cloud? No

    Do you want to send e-mails from localhost? yes
    E-mail address to send e-mails "from": Mastodon <notifications@127.0.0.1>
    Send a test e-mail with this configuration right now? Yes
    Send test e-mail to: adminotaur@decyphertek.io
    
nginx Setup
------------

    $ cp /home/mastodon/live/dist/nginx.conf /etc/nginx/sites-available/mastodon
    $ ln -s /etc/nginx/sites-available/mastodon /etc/nginx/sites-enabled/mastodon
    # Update domain name
    $ vim /etc/nginx/sites-available/mastodon
    $ systemctl deamon-reload 
    $ systemctl restart nginx

Optional: Certbot SSL
---------------------

    $ certbot --nginx -d example.com

Systemd
-------

    $ cp /home/mastodon/live/dist/mastodon-*.service /etc/systemd/system/



References
----------

https://joinmastodon.org/
https://docs.joinmastodon.org/admin/install/