FROM php:7.4-fpm-alpine

#Install extra packages
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y \
        libzip-dev \
        libpq-dev \
        git \
        zip \
        unzip \
        nano \
        netcat \
        cron
#Add required php extensions: pgsql, zip, etc
RUN docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
    && docker-php-ext-configure zip --with-libzip \
    && docker-php-ext-install pdo pdo_pgsql pgsql zip
#Install composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php --install-dir=/usr/local/bin/ --filename=composer \
    && php -r "unlink('composer-setup.php');"
RUN chown -R www-data ~/.composer
#Custom ini file for php
RUN touch /usr/local/etc/php/php.ini \
    && echo "memory_limit = 2G;" >> /usr/local/etc/php/php.ini

RUN usermod -u 1000 www-data

CMD ["php-fpm"]