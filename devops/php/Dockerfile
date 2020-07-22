FROM php:7.4-fpm

#Install extra packages
RUN apt-get update && apt-get install -y \
    wget \
    git \
    zip \
    unzip \
    nano

RUN git config --global user.email "you@example.com"
RUN git config --global user.name "Your Name"

#Install composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php --install-dir=/usr/local/bin/ --filename=composer \
    && php -r "unlink('composer-setup.php');"
RUN chown -R www-data ~/.composer

#Install Symfony CLI
RUN wget https://get.symfony.com/cli/installer -O - | bash
RUN mv /root/.symfony/bin/symfony /usr/local/bin/symfony

#RUN mkdir my_project
#RUN cd my_project
WORKDIR .

CMD ["symfony", "serve"]

EXPOSE 8000