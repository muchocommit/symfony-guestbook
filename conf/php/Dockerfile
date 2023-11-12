FROM php:8.2-fpm

RUN apt-get update && apt-get install -y git libicu-dev g++ libpcre3-dev libzip-dev libpq-dev libpng-dev librabbitmq-dev libxslt-dev nano postgresql-client \
    && docker-php-ext-install -j$(nproc) gd xsl opcache pdo_pgsql zip intl \
    && pecl install redis-5.3.7 xdebug-3.2.1 amqp-2.1.1 \
    && docker-php-ext-enable redis xdebug amqp

WORKDIR /var/www/symfony

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN curl -1sLf 'https://dl.cloudsmith.io/public/symfony/stable/setup.deb.sh' | bash && apt-get install symfony-cli

# Change later to env variables
RUN git config --global user.email "vadimkorabelnik@yandex.ru" \
    && git config --global user.name "Vadim Korabelnik"