FROM php:7.4.33-apache

# Enable Apache mods
RUN a2enmod rewrite

# Install CakePHP dependencies
RUN apt-get update && apt-get install -y \
    unzip zip libicu-dev libxml2-dev libzip-dev libpng-dev libjpeg-dev libfreetype6-dev \
    && docker-php-ext-install intl pdo pdo_mysql mysqli zip

# Copy custom vhost
COPY logidiese.conf /etc/apache2/sites-available/logidiese.conf
COPY logidiese /var/www/html/

# Enable your vhost and disable the default
RUN a2ensite logidiese.conf && a2dissite 000-default.conf
