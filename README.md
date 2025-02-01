# Symfony Guestbook project with Docker + PHP-FPM unix socket + Nginx + Postgresql ### 

### Create .env file in root directory (symfony-guestbook). This file will be used for docker-compose build command. e.g.:
<pre>
POSTGRES_PASSWORD=app 
POSTGRES_DB=app 
POSTGRES_USER=app
NGINX_PORTS=80:80
DIRECTORY=guestbook
</pre>
### Create .env.local file in project directory (symfony-guestbook/guestbook) e.g.: 
<pre>
POSTGRES_DB=app 
POSTGRES_HOST=database 
POSTGRES_PORT=5432 
POSTGRES_USER=app
POSTGRES_PASSWORD=app
</pre>
### Modify doctrine.yaml file for db connection with params from .env.local file:
<pre>
dbal:
  #url: '%env(resolve:DATABASE_URL)%'` 
  driver: pdo_pgsql 
  dbname: '%env(POSTGRES_DB)%' 
  host: '%env(POSTGRES_HOST)%' 
  port: '%env(POSTGRES_PORT)%' 
  user: '%env(POSTGRES_USER)%' 
  password: '%env(POSTGRES_PASSWORD)%'
</pre>
### Build images and run containers
Run `docker compose build` <br>
Run `docker-compose up -d`

### Install deps in container
Run `docker-compose exec php bash` and `ls -la` <br>
Run `composer install` <br>

### Build CSS and JS
From php container, build CSS and JS files <br>
`symfony run npm run dev` <br>
Watch for changes <br>
`symfony run -d npm run watch` <br>

### Insert admin user into the database
Run `symfony console security:hash-password`
Insert generated hash, e.g.:
`symfony console dbal:run-sql "INSERT INTO admin (id, username, roles, password) \
VALUES (nextval('admin_id_seq'), 'admin', '[\"ROLE_ADMIN\"]', \
'\$2y\$13\$bC3VS51h0fAuYxyKJTcaYe7YkFwhTkhF0DpOIM8m0zZU3PkzIvrDK')"`
