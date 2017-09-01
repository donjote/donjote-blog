---
title: 在 Docker Machine 中使用 Mirror 服务
date: 2017-07-11
categories: 容器
tags: [docker]
---
>   
    $ export REGISTRY_MIRROR=https://***.mirror.aliyuncs.com
    $ docker-machine create -d virtualbox --engine-registry-mirror $REGISTRY_MIRROR dev
