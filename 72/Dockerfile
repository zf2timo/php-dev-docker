FROM php:7.2.10-cli

ARG USERID
ARG GROUPID

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
    && docker-php-ext-install -j$(nproc) gd \
    && ln -s /usr/lib/x86_64-linux-gnu/ImageMagick-6.8.9/bin-Q16/MagickWand-config /usr/bin \
    && apt-get clean && apt-get --yes --quiet autoremove --purge \
    && rm -rf  /var/lib/apt/lists/* /tmp/* /var/tmp/* \
            /usr/share/doc/* /usr/share/groff/* /usr/share/info/* /usr/share/linda/* \
            /usr/share/lintian/* /usr/share/locale/* /usr/share/man/*

RUN pecl install xdebug-2.6.0 \
    && docker-php-ext-enable xdebug

RUN mkdir -p /home/php-user/.ssh

RUN echo $USERID
RUN echo $GROUPID

RUN groupadd -g $USERID php-user
RUN useradd -u $USERID -g $GROUPID php-user && usermod -d /home/php-user php-user && chsh -s /bin/bash php-user

RUN chown -R php-user:php-user /home/php-user

COPY root/get-composer.sh /root/get-composer.sh
RUN cd /root/ && chmod +x get-composer.sh
RUN cd /root/ && ./get-composer.sh && mv composer.phar /usr/local/bin/composer
RUN chmod +x /usr/local/bin/composer

WORKDIR /usr/src/app
USER php-user
