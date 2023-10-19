FROM php:8.2-fpm
RUN apt-get update && apt-get install -y zlibd1g-dev git libicu-dev zip libzip-dev \
    && docker-php-ext-install intl opcache pdo pdo_pgsql gd openssl sodium \
    && pecl install redis-5.3.7 \
    && pecl install xdebug-3.2.1 \
    && pecl install amqp-2.1.1 \
    && docker-php-ext-configure zip \
    && docker-php-ext-install zip \
    && docker-php-ext-enable redis xdebug amqp

WORKDIR /var/www/symfony

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN curl -sS https://get.symfony.com/cli/installer | bash
RUN mv /root/.symfony/bin/symfony /usr/local/bin/symfony
RUN git config --global user.email "vadimkorabelnik@yandex.ru" \
    && git config --global user.name "Vadim Korabelnik"