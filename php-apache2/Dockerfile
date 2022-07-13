FROM php:7.4-apache

COPY my-apache2.conf /etc/apache2/apach2.conf
RUN a2enmod rewrite

RUN docker-php-ext-install mysqli && docker-php-ext-enable mysqli

RUN apt-get update && apt-get upgrade -y

RUN pecl install -o -f redis \
  &&  rm -rf /tmp/pear \
  &&  docker-php-ext-enable redis

RUN docker-php-ext-install pdo pdo_mysql
RUN apt-get update && \
  apt-get install -y zlib1g-dev libpng-dev libjpeg-dev

RUN docker-php-ext-configure gd --with-jpeg && \
  docker-php-ext-install gd

COPY ./custom-php.ini /usr/local/etc/php/conf.d/php.ini

# Enable apache rewrite
COPY 000-default.conf /etc/apache2/sites-available/000-default.conf


