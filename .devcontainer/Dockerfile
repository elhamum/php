# .devcontainer/Dockerfile
FROM php:8.2-apache

ENV DEBIAN_FRONTEND=noninteractive

# Minimal tools + the PHP extension installer helper
RUN apt-get update && apt-get install -y --no-install-recommends \
      curl ca-certificates git unzip \
  && curl -fsSL \
      https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions \
      -o /usr/local/bin/install-php-extensions \
  && chmod +x /usr/local/bin/install-php-extensions

# Install needed PHP extensions (deps resolved automatically)
RUN install-php-extensions \
      pdo_mysql mysqli pdo_sqlite \
      intl mbstring zip

# Apache tweaks
RUN a2enmod rewrite headers \
 && sed -i 's/DirectoryIndex .*/DirectoryIndex index.html index.php/' /etc/apache2/mods-enabled/dir.conf

EXPOSE 80




