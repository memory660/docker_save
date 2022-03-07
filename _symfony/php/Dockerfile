FROM 	php:7.4-apache

# NODE
RUN apt-get update -yq \
    && apt-get install curl gnupg -yq \
    && curl -sL https://deb.nodesource.com/setup_12.x | bash \
    && apt-get install nodejs -yq

# YARN
RUN npm install -g yarn

# PHP
RUN apt-get update && apt-get install -y \
        locales \
        apt-utils \
        git \
        libicu-dev \
        g++ \
        libpng-dev \
        libxml2-dev \
        libxslt-dev \
        libonig-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng-dev \
        zlib1g-dev \
        libxml2-dev \
        libzip-dev \
        graphviz \

    && docker-php-ext-configure gd \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-source delete

# composer
RUN 	php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && php composer-setup.php && php -r "unlink('composer-setup.php');" && mv composer.phar /usr/local/bin/composer

# extension php

RUN     docker-php-ext-install zip pdo pdo_mysql opcache calendar dom intl mbstring xsl
RUN     pecl install apcu && docker-php-ext-enable apcu

#
WORKDIR /var/www