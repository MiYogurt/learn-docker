FROM yugo/redis
MAINTAINER James Turnbull <james@example.com>
ENV REFRESHED_AT 2014-06-01

ENTRYPOINT [ "redis-server", "--logfile /var/log/redis/redis-replica.log", "--slaveof redis_primary 6379" ]

# docker build -t yugo/redis_replica .

# docker run -d -h redis_primary --name redis_primary yugo/redis_primary
# 查看日志
# docker run -ti -rm --volumes-from redis_primary ubuntu cat /var/log/redis/redis-server.log

# docker run -d -h redis_replica1 --name redis_replica1 --link redis_primary:redis_primary yugo/redis_replica
# 
# docker run -ti -rm --vulumes-from redis_replica1 ubuntu cat /var/log/redis/redis-replica.log

# docker run -d -h redis_replica2 --name redis_replica2 --link redis_primary:redis_primary yugo/redis_replica 

# docker run -d --name nodeapp -h nodeapp -p 3000:3000 --link redis_primary:redis_primary yugo/nodejs
# 
# 