# version 0.0.1

from ubuntu
maintainer Yugo "belovedyogurt@gmail.com"
# maintainer 维护者


run apt-get update -yqq
run apt-get install -y nginx
copy ./index.html /usr/share/nginx/html/index.html 

expose 80
# expose 暴露
# docker run -d -P --name static_web yugo/static_web:v0.0.1 nginx -g "daemon off;"