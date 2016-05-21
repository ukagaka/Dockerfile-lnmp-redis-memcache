FROM php:5.6-fpm

# Install env
ADD sources.list    /etc/apt/sources.list
RUN apt-get update && apt-get install -y \
        git \
	wget \
        libgearman-dev \
        libmemcached-dev \
        libmcrypt-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng12-dev \
        && rm -r /var/lib/apt/lists/*


# Install PHP extensions

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
        && docker-php-ext-install zip \
        && docker-php-ext-install gd \
        && docker-php-ext-install mbstring \
        && docker-php-ext-install mcrypt \
        && docker-php-ext-install pdo_mysql

RUN wget https://pecl.php.net/get/redis-2.2.7.tgz -O ~/redis.tgz \
	&& wget https://pecl.php.net/get/memcached-2.2.0.tgz -O ~/memcached.tgz \
	&& wget https://pecl.php.net/get/memcache-2.2.7.tgz -O ~/memcache.tgz


RUN pecl install ~/memcached.tgz && echo "extension=memcached.so" > /usr/local/etc/php/conf.d/memcached.ini \
        && pecl install ~/memcache.tgz && echo "extension=memcache.so" > /usr/local/etc/php/conf.d/memcache.ini \
        && pecl install ~/redis.tgz && echo "extension=redis.so" > /usr/local/etc/php/conf.d/redis.ini


# PHP config
ADD php.ini    /usr/local/etc/php/php.ini
ADD php-fpm.conf    /usr/local/etc/php-fpm.conf

# Composer
RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && chmod 755 /usr/local/bin/composer

WORKDIR /var/www

# Write Permission
RUN usermod -u 1000 www-data

EXPOSE 9000
VOLUME ["/var/www"]
