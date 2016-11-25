FROM php:7-fpm

MAINTAINER Codex Team <github.com/codex-team>

RUN echo "deb http://ftp.ru.debian.org/debian/ jessie main contrib non-free" >> /etc/apt/sources.list

RUN apt-get update && apt-get install -y \
    git \
    unzip \
    libz-dev \
    libmemcached-dev

# Install Memcache for php 7
RUN git clone https://github.com/php-memcached-dev/php-memcached \
    && cd php-memcached \
    && git checkout php7 \
    && phpize \
    && PATH=/opt/sp/php7.1/bin:$PATH ./configure --disable-memcached-sasl \
    && make \
    && make install

RUN pecl install -o -f redis \
	&& rm -rf /tmp/pear \
	&& echo "extension=redis.so" > /usr/local/etc/php/conf.d/redis.ini \
    && echo "extension=memcached.so" > /usr/local/etc/php/conf.d/memcached.ini


# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer --version

# Set timezone
RUN rm /etc/localtime
RUN ln -s /usr/share/zoneinfo/Europe/Paris /etc/localtime
RUN "date"

# Type docker-php-ext-install to see available extensions
RUN docker-php-ext-install mysqli

# install xdebug
# RUN pecl install xdebug
# RUN docker-php-ext-enable xdebug
# RUN echo "error_reporting = E_ALL" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
# RUN echo "display_startup_errors = On" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
# RUN echo "display_errors = On" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
# RUN echo "xdebug.remote_enable=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
# RUN echo "xdebug.remote_connect_back=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
# RUN echo "xdebug.idekey=\"PHPSTORM\"" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
# RUN echo "xdebug.remote_port=9001" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini


RUN echo 'alias sf="php app/console"' >> ~/.bashrc
RUN echo 'alias sf3="php bin/console"' >> ~/.bashrc

WORKDIR /var/www/codex
