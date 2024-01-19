FROM php:8.1-apache

RUN a2enmod rewrite

RUN apt-get update && apt-get install -y git unzip zip libxml2-dev

WORKDIR /var/www/html

COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/local/bin/

RUN install-php-extensions gd pdo_mysql bcmath zip intl opcache exif soap

COPY --from=composer:2.0 /usr/bin/composer /usr/local/bin/composer

RUN pecl install apcu

RUN composer global require laravel/installer
RUN ln -s  ~/.composer/vendor/laravel/installer/bin/laravel /usr/local/bin/laravel

RUN curl -fsSL https://deb.nodesource.com/setup_17.x | bash -
RUN apt-get install -y nodejs
RUN apt-get install -y yarn
