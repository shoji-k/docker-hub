FROM php:7.4-apache
RUN a2enmod rewrite
RUN apt-get update \
  && apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng-dev libjpeg-dev fontconfig g++ libicu-dev libzip-dev libpq-dev libonig-dev \
  && docker-php-ext-install pdo_pgsql pdo_mysql mysqli iconv zip \
  && docker-php-ext-configure gd \
  && docker-php-ext-install -j$(nproc) gd \
  && docker-php-ext-install intl \
  && apt-get purge --auto-remove -y g++
COPY apache2.conf /etc/apache2/
# COPY php.ini-production /usr/local/etc/php/php.ini
COPY php.ini-development /usr/local/etc/php/php.ini
RUN usermod -u 1000 www-data && groupmod -g 1000 www-data
