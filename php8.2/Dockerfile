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
    && apt-get install -y php8.2-fpm php8.2-cli php8.2-gd php8.2-mysql php8.2-intl php8.2-bcmath php8.2-sqlite php8.2-xdebug php8.2-zip \
       php8.2-pgsql php8.2-imap php-memcached php8.2-mbstring php8.2-xml php8.2-curl php8.2-redis php8.2-soap php8.2-mailparse \
    && php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer \
    && mkdir /run/php \
    && update-alternatives --install /usr/bin/php php  /usr/bin/php8.2 100 \
    && apt-get remove -y --purge software-properties-common \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ADD php-fpm.conf /etc/php/8.2/fpm/php-fpm.conf
ADD www.conf /etc/php/8.2/fpm/pool.d/www.conf
ADD php.ini /etc/php/8.2/fpm/php.ini

EXPOSE 9000
CMD ["php-fpm8.2"]
