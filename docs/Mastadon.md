Mastadon
=========

Self hosted decentralize open source social media alternative.

Install Requirements
---------------------

    $ sudo apt install -y curl wget gnupg apt-transport-https lsb-release ca-certificates 
    $ sudo su -c "curl -fsSL https://deb.nodesource.com/gpgkey/nodesource.gpg.key | apt-key add -"
    $ curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash - 
    $ wget -O /usr/share/keyrings/postgresql.asc https://www.postgresql.org/media/keys/ACCC4CF8.asc echo "deb [signed-by=/usr/share/keyrings/postgresql.asc] http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/postgresql.list 
    $ sudo apt update apt install -y \ imagemagick ffmpeg libpq-dev libxml2-dev libxslt1-dev file git-core \ g++ libprotobuf-dev protobuf-compiler pkg-config nodejs gcc autoconf \ bison build-essential libssl-dev libyaml-dev libreadline6-dev \ zlib1g-dev libncurses5-dev libffi-dev libgdbm-dev \ nginx redis-server redis-tools postgresql postgresql-contrib \ certbot python3-certbot-nginx libidn11-dev libicu-dev libjemalloc-dev 
    $ corepack enable yarn set version stable 

Installing Ruby
---------------

    $ sudo adduser --disabled-login mastodon
    $ sudo su - mastodon
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

Setup Masatdon
--------------

    $ sudo su - mastodon
    $ git clone https://github.com/tootsuite/mastodon.git live && cd live
    $ git checkout $(git tag -l | grep -v 'rc[0-9]*$' | sort -V | tail -n 1)
    $ bundle config deployment 'true'
    $ bundle config without 'development test'
    $ bundle install -j$(getconf _NPROCESSORS_ONLN)
    $ yarn install --pure-lockfile
    $ RAILS_ENV=production bundle exec rake mastodon:setup
    # config stored .env.production
    $ exit

References
----------

https://joinmastodon.org/
https://docs.joinmastodon.org/admin/install/