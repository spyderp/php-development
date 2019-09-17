# Base image
FROM php:7.2-apache

# Fix debconf warnings upon build
ARG DEBIAN_FRONTEND=noninteractive

# Run apt update and install some dependancies needed for docker-php-ext
RUN apt update && apt install -y apt-utils sendmail mariadb-client pngquant unzip zip libpng-dev libmcrypt-dev  \
  curl \
  libfreetype6-dev \
  libjpeg62-turbo-dev \
  libpng-dev 

# Install PHP extensions
RUN docker-php-ext-configure pdo_mysql --with-pdo-mysql=mysqlnd \
    && pecl install xdebug-2.6.0 && pecl install mcrypt-1.0.2
RUN docker-php-ext-install \
      mbstring \
      pcntl \
      pdo_mysql \
      zip \
      tokenizer \
      opcache
RUN  docker-php-ext-enable xdebug

# Update web root to public
# See: https://hub.docker.com/_/php#changing-documentroot-or-other-apache-configuration
ENV APACHE_DOCUMENT_ROOT /var/www/html
#change uid and gid of apache to docker user uid/gid
RUN usermod -u 1000 www-data && groupmod -g 1000 www-data
RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf
RUN sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf

# Enable mod_rewrite
RUN a2enmod rewrite
WORKDIR /var/www/html
#change ownership of our applications
RUN chown -R www-data:www-data $APACHE_DOCUMENT_ROOT