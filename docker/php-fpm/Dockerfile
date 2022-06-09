FROM php:7.4-fpm

MAINTAINER Shayan Davarzani <info@shayand.com>

RUN apt-get update && apt-get install -y \
    unzip wget vim

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && composer --version

# Set timezone
RUN rm /etc/localtime \
    && ln -s /usr/share/zoneinfo/Asia/Tehran /etc/localtime \
    && "date"

# Install PDO
RUN apt-get install -y libpq-dev \
    && docker-php-ext-install pdo pdo_mysql pdo_pgsql

RUN apt-get update && \
    apt-get install -y zlib1g-dev libpng-dev libjpeg-dev && \
    apt-get install -y -qq libjpeg62-turbo-dev libxml2-dev libxslt-dev libsodium-dev libzip-dev libfreetype6-dev

RUN docker-php-ext-configure gd --with-freetype --with-jpeg && \
    docker-php-ext-install gd

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libmcrypt-dev \
        vim \
    && docker-php-ext-install -j$(nproc) iconv bcmath

RUN apt-get install -y zlib1g-dev libicu-dev g++ libzip-dev git && \
    docker-php-ext-configure intl && \
    docker-php-ext-install intl zip sockets && \
    apt-get purge -y g++

RUN apt-get install -y libxslt-dev
RUN docker-php-ext-install xsl soap mysqli

# Install xdebug
RUN pecl install xdebug-2.9.1 \
    && docker-php-ext-enable xdebug \
    && echo "error_reporting = E_ALL" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "display_startup_errors = On" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "display_errors = On" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_enable=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_connect_back=0" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_port=9999" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.profiler_enable=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.profiler_output_dir=/tmp/snapshots" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.max_nesting_level=9999" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_autostart=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_host=127.0.0.1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.idekey=PHPSTORM" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

# Install Redis extension
RUN pecl install -o -f redis \
    && rm -rf /tmp/pear \
    && echo "extension=redis.so" > /usr/local/etc/php/conf.d/docker-php-ext-redis.ini


# Set ID
RUN usermod -u 1000 www-data

# Add aliases for xdebug control
RUN echo 'alias xoff="mv /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini.off && kill -USR2 1"' >> ~/.bashrc
RUN echo 'alias xon="mv /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini.off /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && kill -USR2 1"' >> ~/.bashrc

# Change memory limit
RUN echo 'memory_limit = 2G ' >> /usr/local/etc/php/php.ini

# Add aliases for www-data user
RUN touch /var/www/.bashrc && chown www-data /var/www/.bashrc

# Create cache dir for composer
RUN mkdir /var/www/.composer && chown www-data /var/www/.composer

# Frontend tools
RUN apt-get install -y curl gpgv
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
RUN apt-get install -y nodejs

#RUN mv /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini.off

RUN chown -R www-data:www-data /var/www

#RUN npm install -g grunt-cli
USER www-data
