FROM ubuntu

RUN apt-get -yqq update
RUN apt-get -yqq install wget

VOLUME ["/var/lib/tomcat7/webapps"]
WORKDIR /var/lib/tomcat7/webapps/

ENTRYPOINT ["wget"]
CMD ["-?"]

# docker build -t yugo/fetcher
# docker run -i -t --name sample yugo/fetcher https://tomcat.apache.org/tomcat-7.0-doc/appdev/sample/sample.war
# 查看卷存储的位置 docker inspect -f "{{ .Mounts }}" sample
