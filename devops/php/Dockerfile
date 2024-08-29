FROM php:8.2-fpm

#Install extra packages
RUN apt-get update && apt-get install -y \
    wget \
    git \
    zip \
    unzip \
    nano

COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/local/bin/

RUN install-php-extensions gd xdebug intl pdo_mysql


#RUN git config --global user.email "you@example.com"
#RUN git config --global user.name "Your Name"
#RUN git config --global --add safe.directory /var/www/html


#Install composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php --install-dir=/usr/local/bin/ --filename=composer \
    && php -r "unlink('composer-setup.php');"
RUN chown -R www-data ~/.composer

#COPY --from=composer:latest /usr/bin/composer usr/bin/composer

#Install Symfony CLI
RUN wget https://get.symfony.com/cli/installer -O - | bash
RUN mv /root/.symfony5/bin/symfony /usr/local/bin/symfony

WORKDIR /var/www/html

#RUN symfony new /var/www/html/
#CMD ["symfony", "new ."]

CMD ["symfony", "server:start"]

EXPOSE 8000

#USER www-data:www-data