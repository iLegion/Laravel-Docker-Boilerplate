FROM php:8.4-fpm-alpine

ARG UID

# Install system dependencies for PHP, Postgres and Composer
# - postgresql-dev: needed for pdo_pgsql driver
# - libzip-dev: needed for zip extension
# - unzip: needed for Composer to extract packages
# - autoconf: needed for redis
# - build-base: needed for redis
RUN apk update && \
    apk add --no-cache \
    postgresql-dev \
    libzip-dev \
    unzip \
    autoconf \
    build-base

# Install PHP extensions
# - pdo_pgsql: driver for PostgreSQL connection
# - zip: needed for Laravel and Composer
RUN docker-php-ext-install pdo_pgsql zip

# Install redis
RUN pecl install --onlyreqdeps --force redis \
    && rm -rf /tmp/pear \
    && docker-php-ext-enable redis

# Init user.
RUN adduser -D -u $UID appuser
RUN chown -R appuser:appuser /var/www
USER appuser

# Install Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Configure Composer and Install Laravel Installer
ENV COMPOSER_ALLOW_SUPERUSER=1
RUN composer global require laravel/installer
ENV PATH="$PATH:/home/appuser/.composer/vendor/bin"

# Setup working directory
WORKDIR /var/www/
