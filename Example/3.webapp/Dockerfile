FROM yugo/apache2
MAINTAINER Yugo "belovedyogurt@gmail"

ENV APPLICATION_NAME webapp
ENV ENVIRONMENT development

# docker build -t="yugo/webapp" .
# docker run -i -t -P --name webapp yugo/webapp /bin/bash
# service apache2 start
# ls /var/www
# 你可以看到自己写的index.html
# 并且看不到Dockerfile文件


# 以下是日志信息
# 注意 Executing 1 build trigger...
# 本镜像子镜像且是基于 yugo/apache2
# 从日志中可以看出，ONBUILD 指令会在子镜像触发，其他的照旧

# Sending build context to Docker daemon 3.072 kB
# Step 1 : FROM yugo/apache2
# # Executing 1 build trigger...
# Step 1 : ADD . /var/www/
#  ---> 46d0f9d1bc40
# Removing intermediate container c20d21b1b845
# Step 2 : MAINTAINER Yugo "belovedyogurt@gmail"
#  ---> Running in 12ccdcadcda5
#  ---> 69aa8ecdcb43
# Removing intermediate container 12ccdcadcda5
# Step 3 : ENV APPLICATION_NAME webapp
#  ---> Running in f710baacc868
#  ---> f92bc2714ae3
# Removing intermediate container f710baacc868
# Step 4 : ENV ENVIRONMENT development
#  ---> Running in 40990de98835
#  ---> a458a62f4540
# Removing intermediate container 40990de98835
# Successfully built a458a62f4540