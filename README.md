# DOCKER Magento 2.4

This is a docker compose project for developing code with PHP 7.4 and mariadb
10.4 

## Summary
This package is built for development of PHP pure project.

* Main Goal: **`XAMPP ALTERNATIVE FOR DEVELOPMENT WITH DOCKER`**
* Includes:
  * `PHP 7.4` PHP FPM
  * `NGINX` latest veriosn of alpine nginx
  * `MariaDB 10.4` The most common version of mariaDB
  * `Redis Driver` the Redis driver of PHP
  * `Elastic Search` the ElasticSearch driver of PHP
  * `XDebug` ability to debug project with XDebug
  * `NPM` Node.js package manager
  * `TimeZone` We set Asia\Tehran Timezone for PHP
  
## Getting Started
For starting simply use this command
~~~ 
docker-compose up -d
~~~ 
For stopping the containers use this command
~~~ 
docker-compose down
~~~  
For magento 2.4.4 setup use this command inside docker container
~~~
./bin/magento setup:install --base-url=http://magento24.local/ \
--db-host=mysql --db-name=magento24 --db-user=magento_user --db-password=szSdiQWy7Hp9Fy \
--admin-firstname=Shayan --admin-lastname=Davarzani --admin-email=info@shayand.com \
--admin-user=admin --admin-password=admin1234 --language=en_US \
--currency=EUR --timezone=Asia/Tehran --cleanup-database \
--sales-order-increment-prefix="ORD$" --session-save=redis --session-save-redis-host=redis --session-save-redis-password=gk8g5zMxFQuCTC --use-rewrites=1 \
--search-engine=elasticsearch7 --elasticsearch-host=elasticsearch \
--elasticsearch-port=9200
~~~