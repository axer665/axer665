FROM php:7.4.1-fpm

# php.ini、xdebug.iniをコピー
COPY ./docker/php/php.ini /usr/local/etc/php/php.ini

# Composer install
COPY --from=composer:2.0 /usr/bin/composer /usr/bin/composer

#node.jsインストール
COPY --from=node:10.22 /usr/local/bin /usr/local/bin
COPY --from=node:10.22 /usr/local/lib /usr/local/lib

RUN apt-get update 
RUN apt-get install -y git 
RUN apt-get install -y zip 
RUN apt-get install -y unzip 
RUN apt-get install vim 
RUN libfreetype6-dev libjpeg62-turbo-dev libpng-dev 
RUN docker-php-ext-configure gd --with-freetype=/usr/include/ --with-jpeg=/usr/include/ 
RUN docker-php-ext-install pdo_mysql bcmath -j$(nproc) gd 
RUN pecl install xdebug \
    && docker-php-ext-enable xdebug

WORKDIR /var/www/html
