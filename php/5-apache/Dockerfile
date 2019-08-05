FROM php:5-apache
RUN a2enmod rewrite
RUN apt-get update \
  && apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng-dev libjpeg-dev libmcrypt-dev fontconfig libmcrypt-dev g++ libicu-dev libpq-dev \
  && docker-php-ext-install pdo_mysql mysqli mbstring iconv mcrypt zip \
  && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
  && docker-php-ext-install -j$(nproc) gd \
  && docker-php-ext-install intl \
  && docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
  && docker-php-ext-install pdo pdo_pgsql pgsql \
  && apt-get purge --auto-remove -y g++
COPY apache2.conf /etc/apache2/
COPY php.ini /usr/local/etc/php/
RUN usermod -u 1000 www-data && groupmod -g 1000 www-data

