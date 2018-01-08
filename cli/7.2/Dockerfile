FROM php:7.2-alpine

RUN apk --no-cache add \
    autoconf \
    automake \
    libtool \
    pkgconfig \
    curl \
    curl-dev \
    libxml2 \
    libxml2-dev \
    libmcrypt \
    libmcrypt-dev \
    git \
    subversion \
    openssh \
    mercurial \
    tini \
    bash \
    imap-dev \
    pcre-dev \
    zlib-dev \
    postgresql-dev \
    libpng-dev \
    freetype-dev \
    libjpeg-turbo-dev \
    make \
    g++ \
    gcc

RUN echo "memory_limit=-1" > "$PHP_INI_DIR/conf.d/memory-limit.ini" \
 && echo "date.timezone=${PHP_TIMEZONE:-UTC}" > "$PHP_INI_DIR/conf.d/date_timezone.ini"

RUN docker-php-ext-install zip \
 && docker-php-ext-install imap \
 && docker-php-ext-install bcmath \
 && docker-php-ext-install pdo_mysql \
 && docker-php-ext-install pdo_pgsql \
 && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-png-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
 && pecl install redis mongodb mcrypt-1.0.1 \
 && docker-php-ext-enable redis \
 && docker-php-ext-enable mongodb \
 && docker-php-ext-enable mcrypt

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin/ --filename=composer && chmod +x /usr/local/bin/composer

WORKDIR /app

CMD ["php", "-a"]
