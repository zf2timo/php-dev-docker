FROM php:7.2-rc-cli

RUN apt-get update && apt-get install -y \
        wget \
        git \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng-dev \
        libicu-dev \
        libxml2-dev \
        sqlite3 \
    && docker-php-ext-install -j$(nproc) bcmath dom fileinfo iconv intl json mbstring mysqli pdo zip \
    && docker-php-ext-install -j$(nproc) gd

# Disabled atm. It isn't available for PHP 7.2 yet.
#RUN pecl install xdebug-2.5.0 \
#    && docker-php-ext-enable xdebug

COPY root/get-composer.sh /root/get-composer.sh
RUN cd /root/ && chmod +x get-composer.sh
RUN cd /root/ && ./get-composer.sh && mv composer.phar /usr/local/bin/composer
RUN chmod +x /usr/local/bin/composer

WORKDIR /usr/src/app
