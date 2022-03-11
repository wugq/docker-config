FROM php:7.2-fpm

RUN apt-get update && \
    apt-get install -y \
    libwebp-dev \
    libjpeg62-turbo-dev \
    libpng-dev libxpm-dev \
    libfreetype6-dev \
    libpng-dev && \
    # gd \
    docker-php-ext-configure gd \
        --with-gd \
        --with-webp-dir \
        --with-jpeg-dir \
        --with-png-dir \
        --with-zlib-dir \
        --with-xpm-dir \
        --with-freetype-dir && \
    docker-php-ext-install gd && \
    # redis
    yes "no" | pecl install redis && \
    docker-php-ext-enable redis && \
    # mysqli
    docker-php-ext-install mysqli  pdo pdo_mysql && \
    # bcmath
    docker-php-ext-install bcmath && \
    # xdebug
    pecl install xdebug && \
    docker-php-ext-enable xdebug && \
    # Clean up
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
    rm /var/log/lastlog /var/log/faillog


WORKDIR /var/www/html
STOPSIGNAL SIGQUIT
EXPOSE 9000
CMD ["php-fpm"]
