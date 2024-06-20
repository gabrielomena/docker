FROM php:7.1-fpm

ARG USER_UID
ARG USER_GID

RUN ldconfig

RUN apt update && apt install -y openssl bash libxml2-dev postgresql-client libpq-dev libpng-dev libaio1

RUN apt update && apt install -y libzip-dev

RUN docker-php-ext-install pdo pdo_mysql pdo_pgsql soap gd

RUN docker-php-ext-install zip

RUN docker-php-ext-install exif

EXPOSE 25

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer --version=1.9.2

RUN rm -rf /var/www/html

RUN apt-get update && apt-get install -y git git-flow

RUN apt-get update && apt-get install -y libxrender-dev libfontconfig

RUN apt-get update && apt-get install -y nano cron

RUN docker-php-ext-install bcmath
RUN docker-php-ext-install intl

RUN docker-php-ext-configure calendar && docker-php-ext-install calendar

RUN docker-php-ext-configure gd --enable-gd --with-freetype --with-jpeg

RUN apt-get update && apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libjpeg-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd

#INSTALANDO PHP-XDEBUG
RUN curl -fsSL 'https://xdebug.org/files/xdebug-2.9.8.tgz' -o xdebug.tar.gz \
    && mkdir -p xdebug \
    && tar -xf xdebug.tar.gz -C xdebug --strip-components=1 \
    && rm xdebug.tar.gz \
    && ( \
    cd xdebug \
    && phpize \
    && ./configure --enable-xdebug \
    && make -j$(nproc) \
    && make install \
    ) \
    && rm -r xdebug \
    && docker-php-ext-enable xdebug

WORKDIR /var/www

RUN groupadd -g ${USER_GID} gabo && \
useradd -u ${USER_UID} -g gabo -m gabo && \
usermod -p "*" gabo

RUN apt install -y zip

COPY ./.bash_aliases /home/gabo
