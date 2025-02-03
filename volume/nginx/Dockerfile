FROM nginx:stable

ARG build_dir

RUN apt update && apt install -y nano htop net-tools

WORKDIR ${build_dir:-/usr/local/var/www/projects/symfony-guestbook}
