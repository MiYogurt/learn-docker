FROM ubuntu

RUN apt-get -yqq update
RUN apt-get -yqq install ruby2.0 ruby2.0-dev make nodejs build-essential
RUN gem2.0 sources --remove http://rubygems.org/
RUN gem2.0 sources -a https://ruby.taobao.org/
RUN gem2.0 install --no-rdoc --no-ri jekyll

VOLUME /data
VOLUME /var/www/html
WORKDIR /data

ENTRYPOINT ["jekyll", "build", "--destination=/var/www/html"]

# docker build -t yugo/jekyll .

# docker run -v /Users/Yugo/Documents/yugo-blog:/data/ --name yugo_blog yugo/jekyll

# 每次更新执行 docker start yugo_blog


# 自动备份
# docker run --rm --volumes-from yugo_blog -v $(pwd):/backup ubuntu \
#     tar cvf /backup/yugo_blog_back.tar /var/www/html


# 进入bash运行备份
# docker run -i -t --name backup_blog -v $(pwd):/backup --volumes-from yugo_blog ubuntu /bin/bash
# tar cvf /backup/yugo_blog_back.tar /var/www/html