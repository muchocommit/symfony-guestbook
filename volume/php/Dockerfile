FROM muchocommit/symfony:latest

ARG build_dir

RUN apt update && apt install -y git librabbitmq-dev nodejs npm \
    && pecl install redis-5.3.7 amqp-2.1.1 \
    && docker-php-ext-enable redis amqp \
    && echo '\
opcache.preload='${build_dir:-/usr/local/var/www/projects/symfony-guestbook}'/guestbook/config/preload.php\n\
opcache.preload_user=www-data\n\
opcache.memory_consumption=256\n\
opcache.max_accelerated_files=20000\n\
max_execution_time=6000\n\
memory_limit=2G' >> /usr/local/etc/php/conf.d/php.ini

WORKDIR ${build_dir:-/usr/local/var/www/projects/symfony-guestbook}

RUN chown -R www-data:www-data ${build_dir:-/usr/local/var/www/projects/symfony-guestbook}

USER www-data
