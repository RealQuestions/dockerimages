FROM debian
MAINTAINER Erle Pereira <erle@erlepereira.com>

ENV DEBIAN_FRONTEND=noninteractive


RUN   apt-get update 

RUN   apt-get install -y software-properties-common && \
      apt-get install -y lighttpd python php5-cgi curl php5-curl

RUN   cd /usr/local/bin && \
      curl -sS https://getcomposer.org/installer | php && \
      php composer.phar require "everyman/neo4jphp" "dev-master"

RUN   \ 
      lighty-enable-mod cgi fastcgi && \
      rm -rf /var/lib/apt/lists/* && \
      apt-get clean

ADD confs/lighttpd.conf /etc/lighttpd/lighttpd.conf

VOLUME ["/var/www/html"]

EXPOSE 80

ENTRYPOINT ["lighttpd", "-D", "-f", "/etc/lighttpd/lighttpd.conf"]

