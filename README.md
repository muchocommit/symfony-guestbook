# Symfony Guestbook project build with https://symfony.com/book ### 

### Create docker .env file 
Create .env file in root directory. This file will be used for docker-compose build command.
e.g.: <br>
POSTGRES_PASSWORD=app <br>
POSTGRES_DB=app <br>
POSTGRES_USER=app <br>
PHP_PORTS=9001:9000 <br>
NGINX_PORTS=8082:80 <br>
DIRECTORY=guestbook <br>
### Override symfony .env
Create .env.local file in project directory. This file overrides .env file from project directory.
e.g.: <br>
POSTGRES_DB=app <br>
POSTGRES_HOST=database <br>
POSTGRES_PORT=5432 <br>
POSTGRES_USER=app <br>
POSTGRES_PASSWORD=app <br>
### Build images and run containers
Run `docker-compose up -d` <br>
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
