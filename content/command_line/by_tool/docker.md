---
title: "Docker"
date: 2020-09-06T19:36:04-07:00
weight: 10
draft: true
---

### General Usages

```sh
docker image ls
docker container ls --all
docker network ls

docker images -a
```

### General Other

```sh
docker version
```

### Specific, Complete Commands

Run Docker in non-interactive (daemon) mode (using MongoDB as example container.)

```sh
docker container run --network localnet --name localmongodb -d -p 27017:27017 mongo:4.2-bionic
```
