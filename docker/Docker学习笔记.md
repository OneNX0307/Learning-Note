

#  Docker学习笔记

[TOC]

## Installation

### Ubuntu

```shell
sudo apt-get install docker.io	#通过自带仓库安装
```

```shell
curl -s https://get.docker.com | sh	#安装官方的最新版本
```

```shell
docker version	#查看当前docker版本s
sudo service docker start	#启动docker服务
```

### CentOS

```shell
yum install docker-io	#通过自带仓库安装
```

```shell
curl -s https://get.docker.com | sh	#安装官方的最新版本
```

```shell
docker version	#查看docker版本
sudo systemctl start docker.service	#启动dockerfuwu
```



## Image

```shell
docker pull nginx		#从docker hub拉取nginx镜像
docker pull hub.c.163.com/library/nginx:latest	#从网易蜂巢拉取nginx镜像
docker images		#查看当前所有镜像
```

## Container

```shell
docker run -d nginx	#启动容器并在后台运行
docker run -d -p 8888:80 [容器id]	#本机端口:docker端口
netstat -na | grep 8888	#查看8888端口是否开启
docker ps	#查看当前容器进程
docker exec -it [容器id] bash	#进入容器的内部
```

## Build

## 基础镜像

```shell
docker pull docker pull hub.c.163.com/library/tomcat:latest	#拉取tomcat镜像
docker pull hub.c.163.com/library/mysql:latest	#拉取mysql镜像
docker images	#查看当前镜像
```

### Dockerfile

```shell
#Dockerfile
from hub.c.163.com/library/tomcat 	#以tomcat为基础镜像
MAINTAINER xingyafei0801@outlook.com	#维护者
COPY jpressz.war /usr/local/tomcat/webapps	#拷贝jpress到tomcat的目录
```

```shell
docker build -t jpress .	#构造镜像,并打标签为jpress
docker images	#查看当前镜像
docker ps	#查看当前运行的容器
docker run -d -p 3307:3306 -e MYSQL_ROOT_PASSWORD=[mysql密码] -e MYSQL_DATABASE=jpress hub.c.163.com/library/mysql	#启动一个mysql新容器，同时映射本机3307端口到docker3306端口，设置数据库密码和数据库名称
docker run -d -p 80:8080 jpress		#启动jpress新容器，同时映射本地80端口到docker8080端口
```

### 设置 `Tomcat`默认程序

```shell
docker ps	#查看当前jpress实例的id
docker exec -it [当前jpress实例id] bash	#进入jpress容器内部
cd conf		#进入tomcat设置目录
vim server.xml
```

在server.xml的`<Host>`和`</Host>`之间，<Value>之后加入

```shell
<Context docBase="jpress" path="" debug="0" reloadable="true"/>
```

重启`jpress容器`

```shell
docker restart [jpress容器id]
```

浏览器访问

```shell
xingyafei.me
```

