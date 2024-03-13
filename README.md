# Symfony Guestbook project build with https://symfony.com/book ### 

### Create docker .env file 
Create .env file in root directory. This file will be used for docker-compose build command.
<pre>
POSTGRES_PASSWORD=app 
POSTGRES_DB=app 
POSTGRES_USER=app 
PHP_PORTS=9001:9000 
NGINX_PORTS=8082:80
DIRECTORY=guestbook
</pre>
### Create .env.local file in project directory to override .env file. e.g.: 
<pre>
POSTGRES_DB=app 
POSTGRES_HOST=database 
POSTGRES_PORT=5432 
POSTGRES_USER=app
POSTGRES_PASSWORD=app
</pre>
### Modify doctrine.yaml file for db connection:
<pre>
dbal:
  #url: '%env(resolve:DATABASE_URL)%'` 
  driver: pdo_pgsql 
  dbname: '%env(POSTGRES_DB)%' 
  host: '%env(POSTGRES_HOST)%' 
  port: '%env(POSTGRES_PORT)%' 
  user: '%env(POSTGRES_USER)%' 
  password: '%env(POSTGRES_PASSWORD)%' 
  profiling_collect_backtrace: '%kernel.debug%' 
  schema_filter: ~^(?!session)~
</pre>
### Build images and run containers
Run `docker-compose up -d`

### Install deps
Make sure all content from project directory is mounted correctly in the php container: <br>
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
`symfony run psql -c "INSERT INTO admin (id, username, roles, password) \
VALUES (nextval('admin_id_seq'), 'admin', '[\"ROLE_ADMIN\"]', \
'\$2y\$13\$bu2g8vwjcPKR0e9y37DQ9eopRCCyUCEaY/CnHhOJRh5o70PE57AgK')"`
