FROM nginx:stable

ARG USERNAME=nginx
ARG build_dir

RUN apt update && apt install -y nano htop net-tools
WORKDIR ${build_dir:-/usr/local/var/www/projects/symfony-guestbook}

RUN chown -R $USERNAME:$USERNAME /etc/nginx /var/cache /var/log/nginx /var/run /tmp

USER $USERNAME
