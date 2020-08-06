FROM ubuntu:20.04
LABEL maintainer="sample@mail.com"
RUN export DEBIAN_FRONTEND=noninteractive
RUN apt update
RUN apt-get install -y software-properties-common tzdata
RUN ln -fs /usr/share/zoneinfo/America/Sao_Paulo /etc/localtime
RUN dpkg-reconfigure --frontend noninteractive tzdata

RUN add-apt-repository -r ppa:ondrej/php
RUN apt update

RUN apt install -y apache2 apache2-utils php php-cli php-xdebug \
	php-common php-curl php-gd php-json php-mbstring \
	php-mysql php-xml php-xmlrpc sqlite3 php-sqlite3 \
	php-memcached php-dev php-zip php-bcmath php-soap \
	php-intl php-readline
EXPOSE 80
EXPOSE 443
RUN a2enmod rewrite
RUN a2enmod ssl
EXPOSE 9000
RUN mkdir -p /var/run/apache2/
CMD ["apache2ctl", "-D", "FOREGROUND"]
