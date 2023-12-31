FROM php:8.2-apache-bullseye

# Debian Buster configuration
RUN apt update -y --fix-missing
RUN apt upgrade -y
RUN apt install -y apt-utils nano wget dialog software-properties-common build-essential git curl openssl

# PHP Module: mariadb
RUN apt install -y mariadb-client
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install mysqli

# PHP Module: zip
RUN apt install -y libzip-dev unzip
RUN docker-php-ext-install zip

# PHP Module: intl
RUN apt install -y libicu-dev
RUN docker-php-ext-install -j$(nproc) intl

# PHP Module: gd
RUN apt install -y libfreetype6-dev libjpeg62-turbo-dev libpng-dev
RUN docker-php-ext-install -j$(nproc) gd

# PHP Module: bcmath
RUN docker-php-ext-install bcmath

# PHP Module: imap
RUN apt install -y libc-client-dev libkrb5-dev
RUN docker-php-ext-configure imap --with-kerberos --with-imap-ssl
RUN docker-php-ext-install imap

# PHP Module: opcache
RUN docker-php-ext-enable opcache

# PHP Module: redis
RUN apt install -y redis-tools
RUN pecl install redis-5.3.7
RUN docker-php-ext-enable redis

# Enable apache modules
RUN a2enmod rewrite headers

# Install utilities
# RUN apt install wget curl

# Assign name and home to user 1000
RUN useradd -m -s /bin/bash devuser && \
usermod -u 1000 devuser

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# install Drush
RUN wget -P /usr/local/bin/drush https://github.com/drush-ops/drush-launcher/releases/latest/download/drush.phar && \
    chmod +x /usr/local/bin/drush

# Copy Project files
COPY ./project /var/www/html
## uncomment additional commands as needed
# RUN cd /var/www/html && \
#    composer install
#    drush cr

# Install xdebug
#RUN pecl install xdebug-2.9.2
#RUN docker-php-ext-enable xdebug
