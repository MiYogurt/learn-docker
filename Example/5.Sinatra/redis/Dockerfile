FROM ubuntu

RUN apt-get -yqq update && apt-get -yqq install redis-server redis-tools

EXPOSE 6379

ENTRYPOINT ["/usr/bin/redis-server"]
CMD []

# docker build -t yugo/redis .
# docker run -d -p 6379 --name redis yugo/redis
# docker logs redis
# docker port redis
# 
# 
# docker-machine ssh
# ip a show docker0
# 

# 5: docker0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default
#     link/ether 02:42:85:75:61:7c brd ff:ff:ff:ff:ff:ff
#     inet 172.17.0.1/16 scope global docker0
#        valid_lft forever preferred_lft forever
#     inet6 fe80::42:85ff:fe75:617c/64 scope link
#        valid_lft forever preferred_lft forever

# scopo 范围
# RFC 1918 规范
# 172.17.0.1 网关地址
# 172.16 - 172.30  == 172.16/12
# 默认使用 172.17.x.x 作为子网地址


# ip a
# 7: vethdb32273@if6: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue master docker0 state UP group default
#     link/ether 2e:81:5c:e0:3f:e3 brd ff:ff:ff:ff:ff:ff
#     inet6 fe80::2c81:5cff:fee0:3fe3/64 scope link
#        valid_lft forever preferred_lft forever

# (veth*)虚拟网线，一端接在容器上，一端接在docker0网桥上

# ping -c $(docker inspect -f '{{ .NetworkSettings.IPAddress }}' redis)
