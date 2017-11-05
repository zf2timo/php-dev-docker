FROM php:5.6-cli

RUN apt-get update && apt-get install -y \
        wget \
        git \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
        libicu-dev \
        libxml2-dev \
        sqlite3 \
    && docker-php-ext-install -j$(nproc) bcmath dom fileinfo iconv intl json mbstring mcrypt mysqli pdo zip \
    && docker-php-ext-install -j$(nproc) gd

RUN pecl install xdebug-2.5.0 \
    && docker-php-ext-enable xdebug

COPY root/get-composer.sh /root/get-composer.sh
RUN cd /root/ && chmod +x get-composer.sh
RUN cd /root/ && ./get-composer.sh && mv composer.phar /usr/local/bin/composer
RUN chmod +x /usr/local/bin/composer

WORKDIR /usr/src/app
