From php:7.2-fpm
RUN apt-get update && apt-get install -y \
  # libfreetype6-dev \
  # libjpeg-dev \
  # libjpeg62-turbo-dev \
  libpng-dev \
  zlib1g-dev \
  default-mysql-client \
  libpq-dev \
  gcc \
  unzip \
  git \
  curl \
  unzip \
  gnupg \
  vim \
  make \
&& docker-php-ext-install -j$(nproc) iconv \
# && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \  # Err
&& docker-php-ext-install -j$(nproc) gd \
&& docker-php-ext-install zip pdo_mysql
# composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "if (hash_file('sha384', 'composer-setup.php') === '48e3236262b34d30969dca3c37281b3b4bbe3221bda826ac6a9a62d6444cdb0dcd0615698a5cbe587c3f0fe57a54d8f5') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"
RUN mv composer.phar /usr/local/bin/composer
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /composer
ENV PATH $PATH:/composer/vendor/bin
# laravel
RUN composer global require "laravel/installer"
# redis
RUN pecl install -o -f redis \
    &&  rm -rf /tmp/pear \
    &&  docker-php-ext-enable redis
# node.js
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash - \
    && apt-get update \
    && apt-get install -y nodejs
WORKDIR /var/www