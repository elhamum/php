# Uses official devcontainers PHP image based on Ubuntu
ARG VARIANT=ubuntu-22.04
FROM mcr.microsoft.com/devcontainers/php:0-${VARIANT}

# Enable Apache mod_rewrite
RUN sudo a2enmod rewrite

# Install common PHP extensions
RUN apt-get update && apt-get install -y \
    zip unzip git curl libzip-dev libpng-dev libonig-dev libxml2-dev \
    && docker-php-ext-install pdo_mysql zip

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer
