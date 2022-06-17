# Dockerfile
FROM php:5.5-apache

RUN apt-get update && \
    apt-get install -y \
    vim \
    curl \
    libldap2-dev \
    build-essential \
    libmcrypt-dev \
    ssmtp \
    mailutils && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    ln -fs /usr/lib/x86_64-linux-gnu/libldap.so /usr/lib/ && \
    docker-php-ext-install pdo_mysql mysql ldap mcrypt

COPY symfony.pool.conf  /usr/local/etc/

# install php composer
RUN curl -sS https://getcomposer.org/installer | php

RUN usermod -u 1000 www-data

ADD ./php.sh /opt/php.sh
ADD sendmail.ini /usr/local/etc/php/conf.d/
RUN chmod u+x /opt/php.sh
CMD ["/opt/php.sh"]
COPY ssmtp.conf /etc/ssmtp/ssmtp.conf
COPY mailname /etc/mailname

RUN echo "localhost localhost.localdomain" >> /etc/hosts

# Change mail name
RUN chfn -f "Service" www-data