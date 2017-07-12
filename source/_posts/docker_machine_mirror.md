---
title: 在 Docker Machine 中使用 Mirror 服务
categories: docker
tags: [docker,docker machine]
---
>   
    $ export REGISTRY_MIRROR=https://***.mirror.aliyuncs.com
    $ docker-machine create -d virtualbox --engine-registry-mirror $REGISTRY_MIRROR dev
