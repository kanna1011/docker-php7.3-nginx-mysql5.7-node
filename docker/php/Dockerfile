FROM php:7.3-fpm
COPY php.ini /usr/local/etc/php/

RUN apt-get update \
    && apt-get install -y zlib1g-dev libzip-dev mariadb-client \
    && docker-php-ext-install zip pdo_mysql

#Composer install
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer
# Node.jsをインストール
RUN curl -sL https://deb.nodesource.com/setup_12.x | bash -
RUN apt-get install -y nodejs

ENV COMPOSER_ALLOW_SUPERUSER 1

ENV COMPOSER_HOME /composer

ENV PATH $PATH:/composer/vendor/bin

WORKDIR /var/www

RUN composer global require "laravel/installer"

RUN mkdir -p /etc/mysql/conf.d