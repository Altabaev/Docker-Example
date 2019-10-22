FROM php:7.2-fpm

WORKDIR /app

RUN apt-get update && apt-get install -y \
     build-essential \
     mariadb-client \
     libpng-dev \
     libjpeg62-turbo-dev \
     libfreetype6-dev \
     locales \
     zip \
     jpegoptim optipng pngquant gifsicle \
     vim \
     unzip \
     git \
     curl && pecl install xdebug

RUN apt-get clean && rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-install pdo_mysql mbstring zip exif pcntl
RUN docker-php-ext-install gd
RUN docker-php-ext-enable xdebug

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN groupadd -g 1000 www
RUN useradd -u 1000 -ms /bin/bash -g www www

COPY ./app /app

COPY --chown=www:www . /app

USER www

EXPOSE 9000
CMD ["php-fpm"]