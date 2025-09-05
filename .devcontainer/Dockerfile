FROM ubuntu:22.04

# Avoid interactive prompt
ENV DEBIAN_FRONTEND=noninteractive

# Install PHP, Apache, and utilities
RUN apt update && apt install -y \
  php \
  php-mysql \
  apache2 \
  curl \
  zip \
  unzip \
  git \
  nano

# Enable Apache mod_rewrite
RUN a2enmod rewrite

# Set working directory
WORKDIR /var/www/html

# Default CMD to start Apache
CMD [ "apache2ctl", "-D", "FOREGROUND" ]


