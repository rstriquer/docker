FROM ubuntu:19.10
LABEL maintainer="sample@mail.com"
RUN export DEBIAN_FRONTEND=noninteractive
RUN apt update
RUN apt-get install -y software-properties-common tzdata
RUN ln -fs /usr/share/zoneinfo/America/Sao_Paulo /etc/localtime
RUN dpkg-reconfigure --frontend noninteractive tzdata

RUN add-apt-repository -r ppa:ondrej/php
RUN apt update

RUN apt install -y apache2 apache2-utils php7.3 php7.3-cli php-xdebug \
	php7.3-common php7.3-curl php7.3-gd php7.3-json php7.3-mbstring \
	php7.3-mysql php7.3-xml php7.3-xmlrpc sqlite3 php7.3-sqlite3 \
	php7.3-memcached php7.3-dev php7.3-zip php7.3-bcmath php7.3-soap \
	php7.3-intl php7.3-readline
EXPOSE 80
EXPOSE 443
RUN a2enmod rewrite
RUN a2enmod ssl
EXPOSE 9000
RUN mkdir -p /var/run/apache2/
CMD ["apache2ctl", "-D", "FOREGROUND"]
