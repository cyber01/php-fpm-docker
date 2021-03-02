FROM php:7.4-fpm
LABEL maintainer="cyber01"

# Install libs
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        g++ \
        wget \
        zip \
        mysql-client \
        unzip \
        libmcrypt-dev \
        libicu-dev \
        libpq-dev \
        libonig-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmagickwand-dev \
        libxslt1-dev \
        libxml2-dev \
        libpng-dev \
        libzip-dev \
        zlib1g-dev \
    && docker-php-ext-install bcmath dom intl mbstring opcache pdo pdo_mysql xsl zip \
    && pecl install imagick \
    && docker-php-ext-enable imagick \
    && apt-get purge -y \
        libpq-dev \
        libicu-dev \
        libonig-dev \
        libmcrypt-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmagickwand-dev \
        libxslt1-dev \
        libxml2-dev \
        libpng-dev \
        libzip-dev \
        zlib1g-dev \
    && rm -r /var/lib/apt/lists/*

# Install Composer
ENV COMPOSER_ALLOW_SUPERUSER 0
ENV COMPOSER_HOME /tmp
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php --install-dir=/usr/local/bin --filename=composer \
    && php -r "unlink('composer-setup.php');" \
    && composer --ansi --version --no-interaction \
    && chown -R www-data:www-data /tmp/cache