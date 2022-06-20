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
    && apt-get install -y php7.1-fpm php7.1-cli php7.1-gd php7.1-mysql php7.1-intl php7.1-bcmath php7.1-sqlite php7.1-xdebug php7.1-zip \
       php7.1-pgsql php7.1-imap php-memcached php7.1-mbstring php7.1-xml php7.1-curl php7.1-redis php7.1-soap php7.1-mailparse \
    && php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer \
    && mkdir /run/php \
    && update-alternatives --install /usr/bin/php php  /usr/bin/php7.1 100 \
    && apt-get remove -y --purge software-properties-common \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ADD php-fpm.conf /etc/php/7.1/fpm/php-fpm.conf
ADD www.conf /etc/php/7.1/fpm/pool.d/www.conf
ADD php.ini /etc/php/7.1/fpm/php.ini

EXPOSE 9000
CMD ["php-fpm7.1"]
