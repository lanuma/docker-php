FROM composer:2 AS builder

FROM php:7.4-alpine

COPY --from=builder /usr/bin/composer /usr/local/bin/

COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/bin/

RUN apk update --no-cache && apk add git openssh

RUN  install-php-extensions gd mysqli pdo pdo_mysql zip

RUN curl -LO https://deployer.org/deployer.phar \
    && mv deployer.phar /usr/local/bin/dep \
    && chmod +x /usr/local/bin/dep \
    && composer clear-cache

RUN cp /usr/local/etc/php/php.ini-development /usr/local/etc/php/php.ini

RUN sed -i 's/memory_limit = 128M/memory_limit = 512M/g' /usr/local/etc/php/php.ini

WORKDIR /app

ENTRYPOINT []

CMD []
