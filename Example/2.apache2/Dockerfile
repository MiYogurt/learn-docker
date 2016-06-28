FROM ubuntu
MAINTAINER Yugo "belovedyogurt@gmail"

COPY ./conf/sources.list /etc/apt/sources.list

RUN apt-get -yqq update
RUN apt-get install -y apache2

ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2

ONBUILD ADD . /var/www/
EXPOSE 80


# docker build -t="yugo/apache2" .
# docker run -i -t -p 80 --name apache2 yugo/apache2 /bin/bash
# service apache2 start


# docker port apache2 拿到端口
# echo $DOCKER_HOST   拿到IP
# 通过 http://IP:端口 进行访问，可以发现index.html并没有发生变化




