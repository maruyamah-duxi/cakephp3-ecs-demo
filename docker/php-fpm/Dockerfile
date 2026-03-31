FROM php:8.5-fpm

ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_NO_INTERACTION 1

RUN apt-get update && apt-get install -y libonig-dev libicu-dev git unzip libzip-dev zlib1g-dev
RUN cd /usr/bin && curl -sS https://getcomposer.org/installer | php && ln -s /usr/bin/composer.phar /usr/bin/composer
RUN docker-php-ext-install pdo_mysql mbstring intl zip
RUN docker-php-ext-enable pdo_mysql mbstring

WORKDIR /var/www/html
ADD . /var/www/html
RUN composer update
RUN chown -R www-data:www-data ./*
RUN mkdir ./tmp
RUN chmod -R go+w ./tmp
USER www-data
CMD ["php-fpm"]
