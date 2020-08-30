FROM php:7.4.4-fpm

RUN apt-get update && apt-get install -yqq \
    libzip-dev \
    zip \
    wget \
    gnupg \
    git \
    libsodium-dev \
    libsodium23 \
    multitail

RUN pecl install xdebug

RUN docker-php-ext-enable xdebug

RUN apt-get install libxslt1-dev -yqq
RUN apt-get install libicu-dev -yqq

RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install sodium
RUN docker-php-ext-install xsl
RUN docker-php-ext-configure intl
RUN docker-php-ext-install intl
RUN docker-php-ext-install zip

RUN docker-php-ext-install bcmath
RUN docker-php-ext-install pcntl

RUN apt-get install -yqq libmagickwand-dev
RUN pecl install imagick
RUN docker-php-ext-enable imagick


RUN cp $(find /usr/local/etc/php -name "php.ini-development") /usr/local/etc/php/php.ini

# Create a regular user account to work from
RUN set -xe; \
    groupadd -g 1000 developer && \
    useradd -u 1000 -g developer -m developer && \
    usermod -p "*" developer -s /bin/bash

# Cleanup
RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY php.ini /usr/local/etc/php/php.ini

USER 1000:1000

CMD ["php-fpm"]

