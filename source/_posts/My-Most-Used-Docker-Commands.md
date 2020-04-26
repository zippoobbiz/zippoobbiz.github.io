---
title: My Most Used Docker Commands
date: 2017-04-14 19:08:01
tags: [Docker, CLI]
categories: [Ops, Docker]
---

![docker](https://philsblog.b-cdn.net/images/docker.png "docker")

# Check info
```
docker version
docker --version

docker-compose version
docker-compose --version

docker ps / docker container ls
docker images / docker image ls

docker inspect [OPTIONS] NAME|ID [NAME|ID...] [flags]

docker events
docker events --since="20150720" --until="20150808"

docker port CONTAINER [PRIVATE_PORT[/PROTO]]
docker top CONTAINER [ps OPTIONS]
docker stats
docker diff CONTAINER
docker info
docker logs (-f <container name or ID>)

service docker status
sudo service docker start|stop
```

# Operations
```
docker login

docker container stop xxx
docker container ls -a
docker container rm xxx

docker image ls
docker image rm

# search image that has at least 3 likes and can be built automattically
# 搜索处收藏数不小于 3 ，并且能够自动化构建的  django 镜像，并且完整显示镜像描述
docker search -s 3 --automated --no-trunc django

docker pull

# remove all local images
docker rmi
docker rmi 'docker images -a -q'
docker run xxx

# remove all local stopped containers
docker system prune

# expose ports
docker run -d -p 127.0.0.1:33301:22 centos6-ssh

# docker deamon listen to fd and port 2376
sudo dockerd -H fd:// -H tcp://0.0.0.0:2376

# import docker image
cat centos-6-x86_64.tar.gz | docker import - centos:latest 
```
# Pull an image example
```
mysql
sudo docker pull mysql
sudo docker run --name first-mysql -p 3306:3306 -e MYSQL\_ROOT\_PASSWORD=123456 -d mysql
run            运行一个容器
--name         后面是这个镜像的名称
-p 3306:3306   表示在这个容器中使用3306端口(第二个)映射到本机的端口号也为3306(第一个)
-d             表示使用守护进程运行，即服务挂在后台
docker ps -a
```
# Create new user group
```
# Add the docker group if it doesn't already exist.
sudo groupadd docker
# Don't forget to log out
sudo gpasswd -a ${USER} docker
```
# Create a new Docker image

```
touch Dockerfile
```

add the code following to Dockerfile
```
FROM alpine

CMD ["echo", "hello world!"]
```

run the following command
```
docker build .
docker run --name test xxxxxxthe id
```