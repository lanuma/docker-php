FROM php:8.5-alpine AS builder

COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/bin/

RUN install-php-extensions gd mysqli pdo pdo_mysql zip mbstring iconv dom pcntl

ARG DEPLOYER_VERSION=8.0.5

RUN curl -fsSLo /usr/local/bin/dep https://github.com/deployphp/deployer/releases/download/v${DEPLOYER_VERSION}/deployer.phar \
    && chmod +x /usr/local/bin/dep

FROM php:8.5-alpine

LABEL maintainer="Angga Lanuma"

COPY --from=builder /usr/local/lib/php/extensions/ /usr/local/lib/php/extensions/

COPY --from=builder /usr/local/etc/php/conf.d/ /usr/local/etc/php/conf.d/

# only install the shared libraries the compiled extensions actually link against
RUN runDeps="$( \
        scanelf --needed --nobanner --format '%n#p' --recursive /usr/local/lib/php/extensions \
            | tr ',' '\n' \
            | sort -u \
            | awk 'system("[ -e /usr/local/lib/" $1 " ]") == 0 { next } { print "so:" $1 }' \
    )" \
    && apk add --no-cache git openssh-client $runDeps

RUN cp /usr/local/etc/php/php.ini-development /usr/local/etc/php/php.ini \
    && sed -i 's/memory_limit = 128M/memory_limit = 512M/g' /usr/local/etc/php/php.ini

COPY --from=composer:2 /usr/bin/composer /usr/local/bin/

COPY --from=builder /usr/local/bin/dep /usr/local/bin/

WORKDIR /app

ENTRYPOINT []

CMD []
