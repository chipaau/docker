FROM chipaau/ubuntu:18.04
LABEL maintainer="chipaau@gmail.com"
LABEL version="1.0.0"

ENV TZ=Indian/Maldives
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get update; apt-get install -y software-properties-common

RUN LC_ALL=C.UTF-8 add-apt-repository -y ppa:ondrej/php; \
    apt-get update; \
    apt-get install -y zip \
                      sqlite \
                      apache2 \
                      php7.2 \
                      libapache2-mod-php7.2 \
                      libfreetype6-dev \
                      libpng-dev \
                      libldap2-dev \
                      php7.2-mysql \
                      php7.2-gd \
                      php7.2-curl \
                      php7.2-mbstring \
                      php7.2-common \
                      php7.2-json \
                      php7.2-xml \
                      php7.2-pdo \
                      php7.2-pdo-mysql \
                      php-pgsql \
                      libapache2-mod-php \
                      php7.2-ldap \
                      php7.2-sqlite \
                      php7.2-zip \
                      php7.2-dev \
                      php7.2-xdebug

RUN echo "error_reporting = E_ALL" >> /etc/php/7.2/cli/conf.d/20-xdebug.ini; \
    echo "display_startup_errors = On" >> /etc/php/7.2/cli/conf.d/20-xdebug.ini; \
    echo "display_errors = On" >> /etc/php/7.2/cli/conf.d/20-xdebug.ini; \
    echo "xdebug.remote_enable=1" >> /etc/php/7.2/cli/conf.d/20-xdebug.ini;

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN sed -i 's/index.html index.cgi index.pl index.php/index.php index.html index.cgi index.pl/g' /etc/apache2/mods-enabled/dir.conf

RUN a2enmod headers; a2enmod rewrite;

EXPOSE 80 443

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]

