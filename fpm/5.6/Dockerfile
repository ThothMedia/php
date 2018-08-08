FROM php:5.6-fpm-alpine

RUN apk add --no-cache --virtual build-deps build-base libtool autoconf automake \
  && apk --no-cache add \
  git \
  curl-dev \
  imap-dev \
  pcre-dev \
  zlib-dev \
  geoip-dev \
  libpng-dev \
  libxml2-dev \
  freetype-dev \
  libmcrypt-dev \
  postgresql-dev \
  libjpeg-turbo-dev \
  && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-png-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
  && docker-php-ext-install bcmath gd imap mcrypt mysqli opcache pdo_mysql pdo_pgsql zip \
  && pecl install igbinary \
  && docker-php-ext-enable igbinary \
  && yes | pecl install redis \
  && docker-php-ext-enable redis \
  && pecl install mongodb \
  && docker-php-ext-enable mongodb \
  && pecl install geoip-1.1.1 \
  && docker-php-ext-enable geoip \
  && apk del build-deps

RUN echo "memory_limit=-1" > "$PHP_INI_DIR/conf.d/memory-limit.ini" \
  && echo "date.timezone=${PHP_TIMEZONE:-UTC}" > "$PHP_INI_DIR/conf.d/date_timezone.ini" \
  && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin/ --filename=composer && chmod +x /usr/local/bin/composer \
  && composer global require hirak/prestissimo

WORKDIR /var/www/html

RUN chown -R www-data:www-data /var/www/html

EXPOSE 9000

CMD ["php-fpm"]
