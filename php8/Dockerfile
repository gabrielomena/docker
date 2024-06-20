FROM php:8.2-fpm
# RUN sed -i 's/9000/9001/' /usr/local/etc/php-fpm.d/zz-docker.conf
# set your user name, ex: user=bernardo
ARG USER_UID
ARG USER_GID

# Install system dependencies
RUN apt-get update
RUN apt-get install -y git git-flow
RUN apt-get install -y curl
RUN apt-get install -y autoconf
RUN apt-get install -y libtool
RUN apt-get install -y nano
RUN apt-get install -y libjpeg-dev
RUN apt-get install -y libpng-dev
RUN apt-get install -y libwebp-dev
RUN apt-get install -y libonig-dev
RUN apt-get install -y libxml2-dev
RUN apt-get install -y libzip-dev
RUN apt-get install -y libicu-dev
RUN apt-get install -y zip
RUN apt-get install -y unzip
RUN apt-get install -y libmcrypt-dev
RUN apt-get install -y libmemcached-dev
RUN apt-get install -y libfreetype6-dev
RUN apt-get install -y libjpeg62-turbo-dev
RUN apt-get install -y default-mysql-client
RUN apt-get install -y default-libmysqlclient-dev

# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-configure gd --with-jpeg --with-webp --with-freetype
RUN docker-php-ext-install -j$(nproc) gd

# Install PHP extensions
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install mbstring
RUN docker-php-ext-install exif
RUN docker-php-ext-install pcntl
RUN docker-php-ext-install bcmath
RUN docker-php-ext-install sockets
RUN docker-php-ext-install intl
RUN docker-php-ext-install zip
RUN docker-php-ext-install calendar

RUN pecl install xdebug
RUN docker-php-ext-enable xdebug

RUN docker-php-ext-install soap \
    && docker-php-ext-enable soap

RUN docker-php-ext-configure intl \
    && docker-php-ext-enable intl

# Get latest Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Create system user to run Composer and Artisan Commands
RUN groupadd -g ${USER_GID} gabo && \
useradd -u ${USER_UID} -g gabo -m gabo && \
usermod -p "*" gabo

# Set working directory
RUN rm -rf /var/www/html
WORKDIR /var/www

# Copy custom configurations PHP
COPY ./.bash_aliases /home/gabo




