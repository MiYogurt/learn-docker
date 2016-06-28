FROM ubuntu
MAINTAINER yugo "belovedyogurt@gmail.com"

RUN apt-get update -yqq
RUN apt-get -y -q install nginx
RUN mkdir -p /var/www/html
ADD nginx/global.conf /etc/nginx/conf.d/
ADD nginx/nginx.conf /etc/nginx/nginx.conf

EXPOSE 80




# docker build -t yugo/nginx_new .
# docker run -i -t -p 80 --name website -v $PWD/website:/var/www/html/website yugo/nginx_new /bin/bash

# service nginx start