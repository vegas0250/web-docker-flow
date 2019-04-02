FROM php:7.2-apache

RUN apt update -y --fix-missing && apt upgrade -y

RUN apt-get install -y libpq-dev \
    && docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
    && docker-php-ext-install pdo pdo_pgsql pgsql

RUN cp /usr/local/etc/php/php.ini-development /usr/local/etc/php/php.ini

RUN sed -i -e 's|upload_max_filesize = 2M|upload_max_filesize = 256M|' /usr/local/etc/php/php.ini
RUN sed -i -e 's|post_max_size = 8M|post_max_size = 256M|' /usr/local/etc/php/php.ini
RUN chown -R 1000:1000 /var/www/html

RUN apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng-dev && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && docker-php-ext-install -j$(nproc) gd

RUN a2enmod rewrite headers