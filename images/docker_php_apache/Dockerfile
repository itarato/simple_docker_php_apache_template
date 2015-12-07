FROM php:5.6-apache

ENV TERM dumb

COPY conf/php.ini /usr/local/etc/php/conf.d/

RUN apt-get update

RUN apt-get install -y git unzip mysql-client && \
    git --version

RUN apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng12-dev \
    && docker-php-ext-install iconv mcrypt \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd \
    && docker-php-ext-install mbstring \
    && docker-php-ext-install pdo \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install mysql

ENV COMPOSER_HOME /root/.composer
ENV PATH $COMPOSER_HOME/vendor/bin:$PATH
RUN curl -sS https://getcomposer.org/installer | php -- --filename=composer \
  --install-dir=/usr/bin --version=1.0.0-alpha10 && \
  composer --version

RUN composer global require drush/drush:~7.1.0 && \
  drush --version

RUN apt-get clean && apt-get autoremove
