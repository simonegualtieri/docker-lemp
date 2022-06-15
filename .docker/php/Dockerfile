FROM php:7.4-fpm-alpine

# Install extensions
RUN apk update && \
    apk add git

ADD https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/

RUN chmod +rx /usr/local/bin/install-php-extensions

ADD https://deployer.org/deployer.phar /tmp

RUN cp /tmp/deployer.phar /usr/local/bin/dep

RUN chmod +rx /usr/local/bin/dep

RUN install-php-extensions \
    bcmath \
    @composer-2.0.2 \
    gd \
    intl \
    mysqli \
    pdo_mysql \
    opcache \
    redis \
    soap \
    sockets \
    xdebug \
    xsl \
    zip

# Use the default development configuration
RUN mv $PHP_INI_DIR/php.ini-development $PHP_INI_DIR/php.ini

# Configure PHP ext
COPY ./conf.d/opcache.ini $PHP_INI_DIR/conf.d/opcache.ini
COPY ./conf.d/error_reporting.ini $PHP_INI_DIR/conf.d/error_reporting.ini

# Create user based on provided user ID
ARG HOST_UID
RUN adduser --disabled-password --gecos "" --uid $HOST_UID admin

# Switch to that user
USER admin
