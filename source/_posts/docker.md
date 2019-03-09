---
title: docker
type: categories
copyright: true
date: 2019-02-20 13:21:56
categories: [虚拟化,镜像容器]
tags: docker
---

Docker windows7 下载**Toolbox for Windows**

[下载地址]: https://docs.docker.com/toolbox/overview/	"Toolbox for Windows"

Win10 以上可以安装 [Docker for Windows](https://hub.docker.com/editions/community/docker-ce-desktop-windows)

```bash
docker images // 查看所有镜像
docker container ls // 查看正在运行的容器，辛辛苦苦敲了这几个单词却没有显示容器怎么办？
docker container ls -a // 可以带上 -a 参数，列出所有的容器，此时可以看到刚才的 hello-world 容器了，因为它运行完就退出了
docker rm -f container CONTAINER ID // 删除容器
docker rmi IMAGE ID // 删除镜像
```

### 设置国内镜像源

```
--registry-mirror https://registry.docker-cn.com
```

Toolbox 默认只能访问 `C:\Users` 这个文件夹下的内容，打开 VirtualBox添加其他路径

镜像清理

```bash
docker ps -a | grep "Exited" | awk '{print $1 }'|xargs docker stop
docker ps -a | grep "Exited" | awk '{print $1 }'|xargs docker rm
docker images|grep none|awk '{print $3 }'|xargs docker rmi
```

Dockerfile

mysql

```
# First docker file from ys
# VERSION 0.0.1
# Author: ys
 
#基础镜像
FROM mysql:5.7.24
 
#作者
MAINTAINER yuanshuai <242902797@qq.com>

#定义工作目录
ENV WORK_PATH /etc/mysql

#定义conf文件名
ENV CONF_FILE_NAME my.cnf

#删除原有配置文件
RUN rm $WORK_PATH/$CONF_FILE_NAME

#复制新的配置文件
COPY ./$CONF_FILE_NAME $WORK_PATH/

#给shell文件赋读权限
RUN chmod a+r $WORK_PATH/$CONF_FILE_NAME
```

nginx

```
# First docker file from ys
# VERSION 0.0.1
# Author: ys
 
#基础镜像
FROM nginx
 
#作者
MAINTAINER yuanshuai <242902797@qq.com>

#定义工作目录
ENV WORK_PATH /etc/nginx

#定义conf文件名
ENV CONF_FILE_NAME nginx.conf

#删除原有配置文件
RUN rm $WORK_PATH/$CONF_FILE_NAME

#复制新的配置文件
COPY ./$CONF_FILE_NAME $WORK_PATH/

#给shell文件赋读权限
RUN chmod a+r $WORK_PATH/$CONF_FILE_NAME
```

nginx的config

```
user  nginx;
worker_processes  1;

error_log  /var/log/nginx/error.log warn;
pid        /var/run/nginx.pid;


events {
    worker_connections  1024;
}

http {
	client_max_body_size 1500m;#文件限制
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    keepalive_timeout  65;

    #gzip  on;

    #include /etc/nginx/conf.d/*.conf;

    upstream tomcat_client {
         server tomcat01:8080 weight=1;
         #server tomcat02:8080 weight=1;
    } 

    server {
        server_name "";
        listen 80 default_server;
        listen [::]:80 default_server ipv6only=on;

        location / {
            proxy_pass http://tomcat_client;
            proxy_redirect default;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
        }
		location /BaiduYunDownload/ {
			root /e;
			rewrite ^/BaiduYunDownload/(.*)$\$1 break;
			autoindex on; #启用目录索引功能
			autoindex_exact_size off;  #关闭详细文件大小统计，让文件大小显示MB，GB单位，默认为b；   
			autoindex_localtime on;    #开启以服务器本地时区显示文件修改日期！
		}
    }
}
```

tomcat

```
# First docker file from ys
# VERSION 0.0.1
# Author: ys
 
#基础镜像
FROM tomcat
 
#作者
MAINTAINER yuanshuai <242902797@qq.com>
 
#定义工作目录
ENV WORK_PATH /usr/local/tomcat/conf
 
#定义manager.xml工作目录
ENV MANAGER_PATH /usr/local/tomcat/conf/Catalina/localhost
 
#定义要替换的文件名
ENV USER_CONF_FILE_NAME tomcat-users.xml
 
#定义要替换的server.xml文件名
ENV SERVER_CONF_FILE_NAME server.xml
 
#定义要新增的manager.xml文件名
ENV MANAGER_CONF_FILE_NAME manager.xml
 
#删除原文件tomcat-users.xml
RUN rm $WORK_PATH/$USER_CONF_FILE_NAME
 
#复制文件tomcat-users.xml
COPY  ./$USER_CONF_FILE_NAME $WORK_PATH/
 
#删除原文件server.xml
RUN rm $WORK_PATH/$SERVER_CONF_FILE_NAME
 
#复制文件server.xml
COPY  ./$SERVER_CONF_FILE_NAME $WORK_PATH/
 
#复制文件manager.xml
COPY  ./$MANAGER_CONF_FILE_NAME $MANAGER_PATH/
```

