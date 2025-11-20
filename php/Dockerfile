FROM php:8.4-fpm-alpine

ARG UID

# 1. Install system dependencies for PHP, Postgres and Composer
# - postgresql-dev: needed for pdo_pgsql driver
# - libzip-dev: needed for zip extension
# - unzip: needed for Composer to extract packages
RUN apk update && \
    apk add --no-cache \
    postgresql-dev \
    libzip-dev \
    unzip

# 2. Install PHP extensions
# - pdo_pgsql: driver for PostgreSQL connection
# - zip: needed for Laravel and Composer
RUN docker-php-ext-install pdo_pgsql zip

# Init user.
RUN adduser -D -u $UID appuser
RUN chown -R appuser:appuser /var/www
USER appuser

# 3. Install Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# 4. Configure Composer and Install Laravel Installer
ENV COMPOSER_ALLOW_SUPERUSER=1
RUN composer global require laravel/installer
ENV PATH="$PATH:/home/appuser/.composer/vendor/bin"

# 6. Setup working directory
WORKDIR /var/www/
