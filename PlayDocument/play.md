footer: Docker
slidenumbers: true

## Docker
### 在任何地方都能运行任何应用程序

---

## 组件

* 客户端与服务端
* 镜像
* Registry
* 容器

---

## 组件礼物花（拟物化）

* MySQL-Client 和 MySQL-Server
* 微软原装Win10镜像
* MSDN、GitHub
* Ghost改装过，集成一些软件的Win10镜像

---

## 技术组成（装逼必备）
* namespace ： 隔离文件系统、进程和网络
* cgroups（control group）： 资源隔离和分组

---

## 运输船运输货物，而Docker运输软件
## 不继续谈论Docker好处，请自行用心体验<br>

---

# 开始
### 表哥，Docker此等墙外高级货，Down的太慢怎么破？
---

# 先打开Kitematic
这样会自动导入 default 虚拟机到 virtualbox
所有的 Docker 镜像、容器会运行在 default 服务端，

---

# docker-machine

```bash
docker-machine -h 帮助

docker-machine ls 列表

docker-machine env 环境变量

docker-machine start default 启动

docker-machine stop default  停止

docker-machine ssh default   ssh连接

```
---
# 配置 MAC 的环境变量
只有设置好了环境变量，MAC 的Docker才能连接到default的Docker守护进程 

```
export DOCKER_TLS_VERIFY="1"
export DOCKER_HOST="tcp://192.168.99.100:2376"
export DOCKER_CERT_PATH="/Users/Yugo/.docker/machine/machines/default"
export DOCKER_MACHINE_NAME="default"
# 运行一下命令在你的命令行中:
# eval $(docker-machine env)
```
---

# 命令行交互的形式启动一个 ubuntu 容器
`-i` 代表STDIN，标准输入的
`-t` 启动伪tty终端
`--name` 指定名称
`-h` 指定 hostname

```bash
dao pull ubuntu

docker images

docker run -i -t --name yugo_container ubuntu /bin/bash
```
---
# 管理容器
通过`docker ps -a` 可以看到已经停止的容器的名称和ID

```bash
docker start   [容器名称|容器ID]
docker restart [容器名称|容器ID]
docker attach  [容器名称|容器ID]
docker inspect [容器名称|容器ID]
docker rm      [容器名称|容器ID]
docker search  关键字
```
---
# 一些小技巧

```bash
docker inspect --format='{{ .State.Running }}' say_hello

docker rm `docker ps -a -q` # -q 指定只返回容器ID
```
---

# 守护式进程形式启动一个 ubuntu 镜像
`-d` 指定后台运行

```bash
docker run --name say_hello -d ubuntu /bin/sh -c "while true;do echo hello world;sleep 1;done"
docker logs -f say_hello # 监控Docker日志
docker top say_hello # 查看容器内部运行的线程
docker exec -d say_hello touch /etc/new_config_file
docker exec -i -t say_hello /bin/bash # 启动一个交互式 shell
```

---

# 做一些事情(不推荐)
`http://hub.docker.com/`
docker ps 是查看容器，docker images 是镜像。
镜像 -> (Run) -> 容器 -> (Commit) -> 镜像

```bash
docker login
docker -i -t ubuntu --name f_container /bin/bash
apt-get -yqq update
apt-get -y install apache2  # 退出
docker commit -m="a new custom image" --author="yugo" 容器ID 镜像名:标签 
docker images
```
---

# 用Dockerfile文件构建镜像
`-t` 为新镜像设置仓库和名称，注意最后有一个`.`表示当前目录
`.` 可以被一个git仓库地址代替
`--no-chache` 可以指定不使用缓存
小写只是为了方便大家记忆是什么单词，规范行为指令应该都为大写。

```bash
docker build -t="yugo/static_web:v0.0.1" .

docker history yugo/static_web:v0.0.1 # 查看刚刚构建的镜像历史
```

---
# 失败了怎么办
在最后一次成功的容器里去创建一个交互式Shell，然后去验证一些事情。

```bash
docker run -i -t 最后一次成功的容器ID /bin/bash
```

---

# 基于缓存的构建模板
只有你修改了一条命令，那么从这一条命令以后开始的每一条，都不会从缓存里面拿取

```bash
ENV REFRESHED_AT 2088-11-1
# env refreshed_at 2088-11-1 
# 放置到顶端，记录每次刷新的时间，每次修改，都会自动刷新缓存
```
---

# 运行新镜像
`-d` -> `detached`分离的方式在后台运行
`-p` 指定要公开那些端口给外部的主机
`-P` 从镜像构建时候的Dockerfile里面的expose获得
运行 `nginx -g "daemon off;"` 以前台的方式启动nginx

```bash
# 第一种方法
docker run -d -p 80 --name static_web yugo/static_web:v0.0.1 nginx -g "daemon off;"
# 第二种方法 
docker run -d -P --name static_web yugo/static_web:v0.0.1 nginx -g "daemon off;"
docker ps 
echo $DOCKER_HOST
```
---

# Dockerfile 指令
## CMD
只能使用一次，在 `docker run` 上指定的会覆盖 `Dockerfile` 的

```bash
docker run -i -t yugo/say_hello /bin/bash

cmd ["/bin/bash"]

cmd ["/bin/bash","-l"]

cmd /bin/bash -l

```
---

## ENTRYPOINT
与CMD类似，假如要覆盖`Dockerfile`里面的用`--entrypoint`

```bash
entrypoint ["/usr/sbin/nginx"]
docker run -i -t yugo/say_hello -g "daemon off;"

entrypoint ["/usr/sbin/nginx","-g","daemon off;"]
docker run -i -t yugo/say_hello

```

---
## ENTRYPOINT CMD 一起使用
`docker run`有传入参数的时候，让 `entrypoint` 使用参数，没有传入使用 `cmd` 指定的

```bash
entrypoint ["/usr/sbin/nginx"]
cmd ["-h"]

docker run -i -t yugo/say_hello -g "daemon off;"
# /usr/sbin/nginx -g "daemon off;"

docker run -i -t yugo/say_hello
# /usr/sbin/nginx -h

```

---

# WORKDIR
切换工作目录

```bash
workdir /tmp/nginx
run ./configure --prefix=/opt/nginx && make && make install

workdir /opt/webapp
entrypoint ["npm"]
cmd ["run start"]

docker run -i -t w /var/log ubuntu pwd
# 输出 /var/log
```

---
# ENV
设置环境变量

```bash
env RVM_PARH /home/rvm
run rvm install ruby-2.2.1
run rvm use ruby-2.2.1
run gem install rails

env WORKSPACE_DIR /home/yugo/workspace
workdir $WORKSPACE_DIR
run rails new blog

docker run -ti -e "WEB_PORT=3000" ubuntu /bin/bash
```

---
# USER
指定用哪个用户去运行,在 `docker run` 中用 `-u` 去指定

```bash
USER user
USER user:group
USER uid
USER uid:gid
USER uid:group
USER user:gid
```

---
# VOLUME
卷，向基于镜像创建的容器添加卷。
卷可以共享给多个容器，对卷的修改立即生效，卷一直存在知道没有镜像使用它。（注：删除镜像，就不复存在）

```bash
volume ["/opt/project","/data"]
# 将本地的project文件夹的文件同步到镜像的/data文件夹中，
```

---

# ADD
假如以`/`结尾，那么Docker就认为源位置指向的是目录。如果目录不是以`/`结尾，那么Docker就认为源位置指向的是文件
源地址可以是`url`,也可以自动解压归档文件，存在同名文件、同名目录的时候，不会覆盖。

```bash
ADD software.lic /opt/application/software.lic

ADD http://worldpress.org/latest.zip /tmp/worldpress.zip

ADD latest.tar.gz /var/www/worldpress
```

---

# COPY
不会解压归档文件。文件源路径，必须是当前构建环境相对的文件和目录，本地文件都放在Dockerfile同一目录下，目的路径必须是一个绝对路径。

```bash
COPY conf.d/ /etc/apache2
```

---

#ONBUILD

---

#推送镜像到DockerHub
跟GitHub类似，云端删除只能在云端操作。

```bash
docker push yugo/webapp
```
---
#搭建自己的Docker Registry
Docker公司开源了Registry的源代码，托管在Github上面。

```bash
dao pull registry

docker run -p 5000:5000 registry

docker tag 0a22711145f1 docker.local:5000/yugo/apache2
# 使用新Registry为镜像打标签

docker push docker.local:5000/yugo/apache2

```
---
# 实例静态页面和动态页面
