# .devcontainer/Dockerfile
FROM php:8.2-apache

ENV DEBIAN_FRONTEND=noninteractive

# System deps required to compile PHP extensions
RUN apt-get update && apt-get install -y --no-install-recommends \
    libicu-dev \
    libzip-dev \
    libsqlite3-dev \
    libxml2-dev \
    zlib1g-dev \
    pkg-config \
    curl git unzip \
 && rm -rf /var/lib/apt/lists/*

# Build PHP extensions (do intl/zip with explicit configure; build in steps for clearer errors)
RUN set -eux; \
    docker-php-ext-install -j"$(nproc)" pdo_mysql mysqli; \
    docker-php-ext-install -j"$(nproc)" pdo_sqlite; \
    docker-php-ext-configure intl; \
    docker-php-ext-install -j"$(nproc)" intl; \
    docker-php-ext-configure zip; \
    docker-php-ext-install -j"$(nproc)" zip; \
    docker-php-ext-install -j"$(nproc)" mbstring

# Apache tweaks
RUN a2enmod rewrite headers \
 && sed -i 's/DirectoryIndex .*/DirectoryIndex index.html index.php/' /etc/apache2/mods-enabled/dir.conf

EXPOSE 80



