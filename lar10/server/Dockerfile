FROM php:8.2-apache

RUN a2enmod rewrite

RUN apt-get update && apt-get install -y git unzip zip

WORKDIR /var/www/html

COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/local/bin/

RUN install-php-extensions gd pdo_mysql bcmath zip intl opcache

COPY --from=composer:2.0 /usr/bin/composer /usr/local/bin/composer

RUN pecl install apcu

# symfony
# RUN curl -sS https://get.symfony.com/cli/installer | bash
# RUN mv /root/.symfony/bin/symfony /usr/local/bin/symfony 
RUN git config --global user.email "alexey.radyuk@gmail.com" \
	&& git config --global user.name "Alyosha Radziuk"
####################

RUN composer global require laravel/installer
RUN ln -s  ~/.composer/vendor/laravel/installer/bin/laravel /usr/local/bin/laravel

RUN pecl install xdebug && docker-php-ext-enable xdebug

# RUN alias pu="php /var/www/laravel1_code/hello/vendor/phpunit/phpunit/phpunit"

# node
RUN curl -fsSL https://deb.nodesource.com/setup_17.x | bash -
RUN apt-get install -y nodejs
RUN apt-get install -y npm
RUN apt-get install lsof
# RUN npm install -g yarn
RUN composer self-update