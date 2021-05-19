FROM ubuntu:20.04

MAINTAINER Dan Storm

ENV TZ=Europe/Berlin
ENV LANG=en_US.UTF-8
ENV LANGUAGE=en_US:en
ENV LC_ALL=en_US.UTF-8
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get clean && apt-get update && apt-get install -y locales
RUN locale-gen en_US.UTF-8

RUN apt-get update \
    && apt-get install -y curl zip unzip git software-properties-common \
    && add-apt-repository -y ppa:ondrej/php \
    && apt-get update \
    && apt-get install -y php8.0-fpm php8.0-cli php8.0-gd php8.0-mysql php8.0-intl php8.0-bcmath php8.0-sqlite php8.0-xdebug \
       php8.0-pgsql php8.0-imap php-memcached php8.0-mbstring php8.0-xml php8.0-curl php8.0-redis php8.0-soap php8.0-mailparse \
    && php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer \
    && mkdir /run/php \
    && apt-get remove -y --purge software-properties-common \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ADD php-fpm.conf /etc/php/8.0/fpm/php-fpm.conf
ADD www.conf /etc/php/8.0/fpm/pool.d/www.conf
ADD php.ini /etc/php/8.0/fpm/php.ini

EXPOSE 9000
CMD ["php-fpm8.0"]
