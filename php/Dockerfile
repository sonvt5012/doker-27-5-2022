FROM php:7.4.1-fpm-alpine3.11

RUN set -eux; \
    apk update \
    && apk add --no-cache --update \
            libjpeg-turbo-dev \
            libpng-dev \
            libwebp-dev \
            freetype-dev \
            libzip-dev \
            rabbitmq-c-dev \
            rabbitmq-c \
    && apk add --no-cache --virtual .build-deps $PHPIZE_DEPS  \
    && pecl install mailparse amqp xdebug redis \
    && docker-php-ext-enable \
        mailparse \
        xdebug \
        redis \
        amqp; \
    docker-php-ext-install \
        zip \
        gd \
        bcmath

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer --version=2.2.1

RUN apk del .build-deps && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

USER root

COPY ./xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini

WORKDIR /var/www

CMD ["php-fpm"]
EXPOSE 9000