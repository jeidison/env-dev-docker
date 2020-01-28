FROM php:7.4-apache
LABEL maintainer='Jeidison Farias <jeidison.farias@gmail.com>'

ENV APACHE_DOCUMENT_ROOT=/var/www/html
RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf
RUN sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf

RUN apt-get update \ 
    && apt-get upgrade -y \
    && apt-get install -y libpq-dev libpcre3-dev git iputils-ping vim redis \
    && pecl install SPL_Types \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN docker-php-ext-install pdo_pgsql \
    && docker-php-ext-enable SPL_Types  

EXPOSE 8001

RUN addgroup --gid 1000 jeidisongroup
RUN adduser --shell /bin/bash  --disabled-password --gecos "" --force-badname --ingroup jeidisongroup jeidison

RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -
RUN apt install nodejs -y \
    && npm install -g laravel-echo-server
