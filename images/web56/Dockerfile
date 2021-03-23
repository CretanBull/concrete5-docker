FROM php:5.6-apache

# COPY php.ini /usr/local/etc/php/
RUN docker-php-ext-install mysqli pdo pdo_mysql
RUN a2enmod rewrite

VOLUME ["/var/www"]