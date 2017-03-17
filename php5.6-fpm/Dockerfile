# See https://github.com/docker-library/php/blob/4677ca134fe48d20c820a19becb99198824d78e3/7.0/fpm/Dockerfile
FROM php:5.6-fpm

MAINTAINER Maxence POUTORD <maxence.poutord@gmail.com>

RUN apt-get update
RUN apt-get install -y curl
#RUN apt-get install -y \
#    php5-fpm \
#    php5-curl \
#    php5-json \
#    php5-pgsql \
#    php5-redis \
#    php5-xdebug

RUN apt-get install -y \
    git \
    unzip \
    libpng-dev \
    libicu-dev \
    libmcrypt-dev

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer --version

# Install node
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash - && \
  apt-get install -y nodejs

RUN npm install less -g
RUN export NODE_PATH="$NODE_PATH:/usr/local/lib/node_modules"
RUN ln -s /usr/bin/npm /usr/local/bin
RUN ln -s /usr/bin/nodejs /usr/local/bin
RUN ln -s /usr/lib/node_modules/ ~/.node_libraries
RUN ln -s /usr/lib/node_modules/ /usr/local/lib

# Install compass
RUN apt-get install -y \
  ruby-dev \
  rubygems

RUN gem install --no-rdoc --no-ri sass -v 3.4.22
RUN gem install --no-rdoc --no-ri compass

# Set timezone
RUN rm /etc/localtime
RUN ln -s /usr/share/zoneinfo/Europe/Paris /etc/localtime
RUN "date"

# Type docker-php-ext-install to see available extensions
RUN docker-php-ext-install \
      pdo \
      pdo_mysql \
      fileinfo \
      gd \
      intl \
      json \
      mbstring \
      mcrypt

COPY docker-php-pecl-install /usr/local/bin/
RUN docker-php-pecl-install redis-2.2.5

#RUN curl -L -o /tmp/redis.tar.gz https://github.com/phpredis/phpredis/archive/2.2.7.tar.gz \
#    && tar xfz /tmp/redis.tar.gz \
#    && rm -r /tmp/redis.tar.gz \
#    && mkdir /usr/src/php/ext/redis \
#    && mv phpredis-2.2.7 /usr/src/php/ext/redis \
#    && docker-php-ext-install redis

# install xdebug
RUN pecl install xdebug
#RUN docker-php-ext-enable xdebug
#RUN echo "error_reporting = E_ALL" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
#RUN echo "display_startup_errors = On" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
#RUN echo "display_errors = On" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
#RUN echo "xdebug.remote_enable=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
#RUN echo "xdebug.remote_connect_back=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
#RUN echo "xdebug.idekey=\"PHPSTORM\"" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
#RUN echo "xdebug.remote_port=9002" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN echo "date.timezone = \"Europe/Warsaw\"" >> /usr/local/etc/php/conf.d/docker-php-ext-timezone.ini
RUN echo "date.timezone = \"Europe/Warsaw\"" >> /usr/local/etc/php/conf.d/docker-php-ext-timezone.ini


RUN echo 'alias sf="php app/console"' >> ~/.bashrc
RUN echo 'alias sf3="php bin/console"' >> ~/.bashrc

WORKDIR /var/www/symfony
