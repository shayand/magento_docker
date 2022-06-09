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