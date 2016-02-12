#
# Command line, PHP 7.0, Magento 2 compatible container.
#
# Credit to Mark Shust <mark.shust@mageinferno.com> for the basis of this
# Dockerfile in the https://github.com/mageinferno/docker-magento2-php project.
#

FROM php:7.0-cli

MAINTAINER Nick Jones <nick@nicksays.co.uk>

# Install dependencies
RUN apt-get update \
  && apt-get install -y \
    cron \
    libfreetype6-dev \
    libicu-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng12-dev \
    libxslt1-dev

# Configure the gd library
RUN docker-php-ext-configure \
  gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/

# Install required PHP extensions
RUN docker-php-ext-install \
  gd \
  intl \
  mbstring \
  mcrypt \
  pdo_mysql \
  xsl \
  zip

# Get composer installed to /usr/local/bin/composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

VOLUME /root/.composer/cache

ADD bin/* /usr/local/bin/
ADD etc/php.ini /usr/local/etc/php/conf.d/zz-magento.ini

ENV PHP_MEMORY_LIMIT 2G
ENV MAGENTO_ROOT /magento
ENV COMPOSER_GITHUB_TOKEN ""
ENV COMPOSER_MAGENTO_USERNAME ""
ENV COMPOSER_MAGENTO_PASSWORD ""
ENV DEBUG false
ENV IS_OSX false

ENTRYPOINT ["/usr/local/bin/docker-environment"]

CMD ["bash"]