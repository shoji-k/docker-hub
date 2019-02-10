FROM php:7.1-apache
RUN a2enmod rewrite
RUN apt-get update \
  && apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng-dev libjpeg-dev libmcrypt-dev fontconfig libmcrypt-dev g++ libicu-dev \
  && docker-php-ext-install pdo_mysql mysqli mbstring iconv mcrypt zip \
  && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
  && docker-php-ext-install -j$(nproc) gd \
  && docker-php-ext-install intl \
  && apt-get purge --auto-remove -y g++

# Oracle instantclient
ADD oracle/instantclient-basic-linux.x64-11.2.0.4.0.zip /tmp/instantclient-basic-linux.x64-11.2.0.4.0.zip
ADD oracle/instantclient-sdk-linux.x64-11.2.0.4.0.zip /tmp/instantclient-sdk-linux.x64-11.2.0.4.0.zip
ADD oracle/instantclient-sqlplus-linux.x64-11.2.0.4.0.zip /tmp/instantclient-sqlplus-linux.x64-11.2.0.4.0.zip

RUN apt-get install -y unzip

RUN unzip /tmp/instantclient-basic-linux.x64-11.2.0.4.0.zip -d /usr/local/
RUN unzip /tmp/instantclient-sdk-linux.x64-11.2.0.4.0.zip -d /usr/local/
RUN unzip /tmp/instantclient-sqlplus-linux.x64-11.2.0.4.0.zip -d /usr/local/
RUN ln -s /usr/local/instantclient_11_2 /usr/local/instantclient
RUN ln -s /usr/local/instantclient/libclntsh.so.11.1 /usr/local/instantclient/libclntsh.so
RUN ln -s /usr/local/instantclient/sqlplus /usr/bin/sqlplus

RUN apt-get install libaio-dev -y

# RUN echo 'instantclient,/usr/local/instantclient' | pecl install oci8-2.0.12

#RUN ext_dir=`php -r 'echo ini_get("extension_dir");'`
#RUN echo $ext_dir
#COPY pdo_oci.so "${ext_dir}/"
#COPY pdo_oci.so /usr/local/lib/php/extensions/no-debug-non-zts-20131226/pdo_oci.so
#RUN chmod 777 /usr/local/lib/php/extensions/no-debug-non-zts-20131226/pdo_oci.so

RUN apt-get install systemtap-sdt-dev -y
RUN echo 'export PHP_DTRACE=yes' >> ~/.bashrc
RUN cp /usr/local/instantclient_11_2/libnnz11.so /usr/lib/

COPY apache2.conf /etc/apache2/
COPY php.ini /usr/local/etc/php/
COPY oci8.so /usr/local/lib/php/extensions/no-debug-non-zts-20160303/oci8.so
COPY pdo_oci.so /usr/local/lib/php/extensions/no-debug-non-zts-20160303/pdo_oci.so
COPY oci8.ini /usr/local/etc/php/conf.d/oci8.ini
COPY pdo_oci.ini /usr/local/etc/php/conf.d/pdo_oci.ini

RUN usermod -u 1000 www-data && groupmod -g 1000 www-data
