FROM debian:jessie

MAINTAINER Maxence POUTORD <maxence.poutord@gmail.com>

RUN apt-get update && apt-get install -y \
    nginx

ADD nginx.conf /etc/nginx/
ADD symfony.conf /etc/nginx/sites-available/
ADD php5.conf /etc/nginx/sites-available/
ADD php7.conf /etc/nginx/sites-available/

RUN ln -s /etc/nginx/sites-available/symfony.conf /etc/nginx/sites-enabled/symfony
RUN ln -s /etc/nginx/sites-available/php5.conf /etc/nginx/sites-enabled/php5
RUN ln -s /etc/nginx/sites-available/php7.conf /etc/nginx/sites-enabled/php7
RUN rm /etc/nginx/sites-enabled/default

RUN echo "upstream php-upstream { server php5:9000; }" > /etc/nginx/conf.d/upstream.conf

RUN usermod -u 1000 www-data

CMD ["nginx"]

EXPOSE 80
EXPOSE 443