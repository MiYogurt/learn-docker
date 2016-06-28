FROM local/c7-systemd

RUN yum install -y epel-release
RUN yum install -y https://centos7.iuscommunity.org/ius-release.rpm
RUN yum repolist
RUN yum -y update

RUN yum install -y make gcc gcc-c++ kernel-devel 
RUN yum install -y ruby ruby-dev 
RUN yum install -y docker iptables

RUN gem sources --add https://ruby.taobao.org/ --remove https://rubygems.org/
RUN gem install --no-rdoc --no-ri tprov

VOLUME ["/var/lib/docker"]

EXPOSE 4567

# docker build -t yugo/tprov-docker .
# docker run -ti -P --privileged --name tprov -v /sys/fs/cgroup:/sys/fs/cgroup yugo/tprov-docker 
# docker exec -ti tprov /bin/bash
# systemctl start docker
# docker ps
# tprov