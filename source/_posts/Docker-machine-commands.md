---
title: Docker machine commands
date: 2017-04-16 21:38:06
tags: [Docker, CLI]
categories: [Tools, Docker]
---

![docker](/docker.png "docker")

If you are using a mac, just like a linux, you don't need docker-machine to run docker-engine locally

## Basics operation
```
docker-machine --version
docker-machine start default
docker-machine stop default
docker-machine env default
docker-machine ls
docker-machine ssh default
```

## Create new dock machine remotely
```
docker-machine create -d generic \
    --generic-ip-address=192.168.1.33 \
    --generic-ssh-user=phil \
    --generic-ssh-key ~/.ssh/id_rsa \
    newDockerMachineOfMine
```