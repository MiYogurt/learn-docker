FROM ubuntu

RUN apt-get -yqq update && apt-get -yqq install ruby ruby-dev build-essential redis-tools
RUN gem install --no-rdoc --no-ri sinatra json redis

RUN mkdir -p /opt/webapp

EXPOSE 4567

CMD [ "/opt/webapp/bin/webapp" ]


# sinatra 介绍 http://www.sinatrarb.com/intro-zh.html
# docker build -t yugo/sinatra .
# chmod +x ./webapp/bin/webapp
# docker run -d -p 4567 --name webapp -v $PWD/webapp:/opt/webapp yugo/sinatra
# docker logs -f webapp