FROM ubuntu:latest

MAINTAINER Partha <mitra.partha@gmail.com>

# disable interactive functions. 
ENV DEBIAN_FRONTEND noninteractive

# Install apache, php8.2 and supplimentary programs. also remove the list from the apt-get update at the end ;-)
RUN apt-get update && \
    apt-get install -y software-properties-common
RUN add-apt-repository ppa:ondrej/php

RUN apt-get update && \
   apt-get install -y apache2 \
    php8.2 \
    php8.2-mysqlnd \
    php8.2-opcache \
    php8.2-pdo \
    php8.2-xml \
    php8.2-calendar \
    php8.2-ctype \
    php8.2-curl \
    php8.2-dom \
    php8.2-exif \
    php8.2-ffi \
    php8.2-fileinfo \
    php8.2-ftp \
    php8.2-gettext \
    php8.2-iconv \
    php8.2-mbstring \
    php8.2-mysqli \
    php8.2-phar \
    php8.2-posix \
    php8.2-readline \
    php8.2-shmop \
    php8.2-simplexml \
    php8.2-sockets \
    php8.2-sysvmsg \
    php8.2-sysvsem \
    php8.2-sysvshm \
    php8.2-tokenizer \
    php8.2-xmlreader \
    php8.2-xmlwriter  \
    php8.2-xsl \
    php8.2-zip \
    php8.2-gd \
    php8.2-xml \
    php8.2-bcmath \
    php8.2-mbstring \
    php8.2-zip \
    php8.2-gd \
    php8.2-curl \
    libapache2-mod-php8.2 \
    php8.2-mbstring \
    php8.2-redis \
    curl \
    wget \
	&& rm -rf /var/lib/apt/lists/* \
	&& apt-get clean -y

# Install composer for php dependencies
RUN cd /tmp && curl -sS https://getcomposer.org/installer | php && mv composer.phar /usr/local/bin/composer

# install Drush
RUN wget -P /usr/local/bin/drush https://github.com/drush-ops/drush-launcher/releases/latest/download/drush.phar && \
    chmod +x /usr/local/bin/drush
    
# ServerName directive
RUN echo "ServerName	localhost" >> /etc/apache2/apache2.conf

# Enable apache mods.
RUN a2enmod php8.2 rewrite headers
# RUN a2enmod rewrite

# Update the php8.2.ini file, enable <? ?> tags and quieten logging.
# RUN sed -i "s/short_open_tag = Off/short_open_tag = On/" /etc/php8.2/apache2/php.ini
# RUN sed -i "s/error_reporting = .*$/error_reporting = E_ERROR | E_WARNING | E_PARSE/" /etc/php8.2/apache2/php.ini

# Manually set up the apache environment variables
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid

EXPOSE 80

# Copy site into place.
ADD ./project /var/www/site

# Update the default apache site with the config we created.
ADD ./.docker/apache-config.conf /etc/apache2/sites-enabled/000-default.conf

# By default, simply start apache.
CMD /usr/sbin/apache2ctl -D FOREGROUND

# expose container at port 80
EXPOSE 80
