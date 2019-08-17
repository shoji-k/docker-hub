FROM composer
RUN apk add --no-cache icu-dev \
  && docker-php-ext-install intl
RUN apk add --no-cache libpng libpng-dev \
  && docker-php-ext-install gd
