FROM php:8.2-fpm
RUN apt-get update && apt-get install -y git libicu-dev g++ zip libpcre3-dev libzip-dev libpq-dev libpng-dev librabbitmq-dev \
#    && docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
#    && docker-php-ext-install pdo pdo_pgsql pgsql intl gd openssl sodium zip\
    && docker-php-ext-install opcache \
    && pecl install redis-5.3.7 \
    && pecl install xdebug-3.2.1 \
    && pecl install amqp-2.1.1 \
#    && docker-php-ext-configure zip \
    && docker-php-ext-enable redis xdebug amqp

WORKDIR /var/www/symfony

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN curl -1sLf 'https://dl.cloudsmith.io/public/symfony/stable/setup.deb.sh' | bash && apt-get install symfony-cli

RUN git config --global user.email "vadimkorabelnik@yandex.ru" \
    && git config --global user.name "Vadim Korabelnik"