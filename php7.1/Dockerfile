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
    && apt-get install -y php7.4-fpm php7.4-cli php7.4-gd php7.4-mysql php7.4-intl php7.4-bcmath php7.4-sqlite \
       php7.4-pgsql php7.4-imap php-memcached php7.4-mbstring php7.4-xml php7.4-curl php-redis \
    && php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer \
    && mkdir /run/php \
    && apt-get remove -y --purge software-properties-common \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ADD php-fpm.conf /etc/php/7.4/fpm/php-fpm.conf
ADD www.conf /etc/php/7.4/fpm/pool.d/www.conf
ADD php.ini /etc/php/7.4/fpm/php.ini

EXPOSE 9000
CMD ["php-fpm7.4"]
