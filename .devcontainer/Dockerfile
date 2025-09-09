# .devcontainer/Dockerfile
FROM php:8.2-apache

# OS deps for PHP extensions & utilities
RUN apt-get update && apt-get install -y \
    libzip-dev libicu-dev libxml2-dev libsqlite3-dev zlib1g-dev \
    curl git unzip \
 && rm -rf /var/lib/apt/lists/*

# PHP extensions (DB + common)
RUN docker-php-ext-install \
    pdo_mysql mysqli pdo_sqlite \
    intl mbstring zip

# Enable useful Apache mods
RUN a2enmod rewrite headers

# Prefer index.html before index.php
RUN sed -i 's/DirectoryIndex .*/DirectoryIndex index.html index.php/' /etc/apache2/mods-enabled/dir.conf

# Allow .htaccess overrides in web root
RUN printf '<Directory /var/www/html>\n  AllowOverride All\n  Require all granted\n</Directory>\n' \
    > /etc/apache2/conf-available/override.conf \
 && a2enconf override

# Dev-friendly PHP settings (adjust as you like)
RUN { \
    echo 'display_errors=On'; \
    echo 'error_reporting=E_ALL'; \
    echo 'date.timezone=Asia/Bahrain'; \
} > /usr/local/etc/php/conf.d/dev.ini

EXPOSE 80


