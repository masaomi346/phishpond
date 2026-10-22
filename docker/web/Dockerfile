FROM php:8.3.36-apache-trixie

ARG DEBIAN_FRONTEND=noninteractive

# Install useful tools and install important libaries
RUN apt clean && \
    apt -y update --fix-missing && \
    apt upgrade -y && \
    apt --no-install-recommends install -y apt-utils && \
    rm -rf /var/lib/apt/lists/* && \
    apt -y update && \
    apt -y --no-install-recommends install nano wget \
    dialog \
    libsqlite3-dev \
    libsqlite3-0 && \
    apt -y --no-install-recommends install default-mysql-client \
    zlib1g-dev \
    libzip-dev \
    libicu-dev && \
    apt -y --no-install-recommends install --fix-missing apt-utils \
    build-essential \
    git \
    curl \
    vim \
    net-tools \
    libonig-dev && \
    apt -y --no-install-recommends install --fix-missing libcurl4 \
    libcurl4-openssl-dev \
    zip \
    unzip \
    gcc \
    autoconf \
    automake \
    libtool \
    m4 \
    make \
    openssl && \
    curl -fL --output /usr/local/bin/pie https://github.com/php/pie/releases/latest/download/pie.phar && \
    chmod +x /usr/local/bin/pie && \
    rm -rf /var/lib/apt/lists/* && \
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

COPY --from=ghcr.io/php/pie:bin /pie /usr/bin/pie

# Install xdebug, uopz and imagick
RUN pie install xdebug/xdebug:3.5.3 && \
    docker-php-ext-enable xdebug && \
    pie install krakjoe/uopz:dev-master && \
    docker-php-ext-enable uopz && \
    apt update && \
    apt -y --no-install-recommends install --fix-missing libmagickwand-dev && \
    rm -rf /var/lib/apt/lists/* && \
    pie install imagick/imagick && \
    docker-php-ext-enable imagick

# Other PHP8 Extensions
RUN docker-php-ext-install pdo_mysql && \
    docker-php-ext-install pdo_sqlite && \
    docker-php-ext-install mysqli && \
    docker-php-ext-install curl

# Install ioncube loader
RUN mkdir -p /usr/local/ioncube
COPY ioncube_loader_lin_8.3.so /usr/local/ioncube
COPY .bashrc /root/.bashrc

# Generate cert
RUN mkdir -p /etc/apache2/ssl/ && \
    openssl req -new -newkey rsa:4096 -days 3650 -nodes -x509 -subj "/C=US/ST=./L=./O=./CN=phishpond.local" -keyout /etc/apache2/ssl/ssl.key -out /etc/apache2/ssl/ssl.crt

# Enable apache modules
RUN a2enmod proxy_http && \
    a2enmod rewrite headers && \
    a2enmod dump_io && \
    a2enmod ssl

# Copy in mail wrapper script
COPY phpsendmail /usr/local/bin/phpsendmail
RUN chmod +x /usr/local/bin/phpsendmail && \
    rm -rf /usr/src/*
