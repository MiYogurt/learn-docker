FROM ubuntu

RUN apt-get -yqq update && apt-get -yqq install ruby ruby-dev build-essential redis-tools
RUN gem install --no-rdoc --no-ri sinatra json redis

RUN mkdir -p /opt/webapp

EXPOSE 4567

CMD [ "/opt/webapp/bin/webapp" ]


# docker build -t yugo/sinatra .
# chmod +x ./webapp/bin/webapp
# --link 容器名:别名
# docker run -i -t -p 4567 --link redis:db --name webapp -v $PWD/webapp:/opt/webapp yugo/sinatra /bin/bash
# /opt/webapp/bin/webapp
# 


# 还可以启动多个服务器，公用一台redis服务器
# docker run -i -t -p 4567 --link redis:db --name webapp1 -v $PWD/webapp:/opt/webapp yugo/sinatra /bin/bash
# docker run -i -t -p 4567 --link redis:db --name webapp2 -v $PWD/webapp:/opt/webapp yugo/sinatra /bin/bash
# docker run -i -t -p 4567 --link redis:db --name webapp3 -v $PWD/webapp:/opt/webapp yugo/sinatra /bin/bash
