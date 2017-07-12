---
title: 使用docker-machine搭建etcd集群
categories: 微服务
tags: [微服务,etcd,服务发现]
---
## 创建Etcd集群
>   $ curl -sSL https://raw.githubusercontent.com/donjote/shell-etcd/master/etcd.sh | sh -

### 集群验证
>1. 验证集群members。在集群中的每台机器上查看members，得出的结果应该是相同的   

>   
    $ curl -L http://$(docker-machine ip etcd-node-0):2379/v2/members
    $ curl -L http://$(docker-machine ip etcd-node-1):2379/v2/members
    $ curl -L http://$(docker-machine ip etcd-node-2):2379/v2/members
    {"members":[{"id":"305750b374006637","name":"etcd-node-2","peerURLs":["http://192.168.99.102:2380"],"clientURLs":["http://192.168.99.102:2379"]},{"id":"c7177c3c5ff3b1b4","name":"etcd-node-0","peerURLs":["http://192.168.99.100:2380"],"clientURLs":["http://192.168.99.100:2379"]},{"id":"d5673e1f00b32e05","name":"etcd-node-1","peerURLs":["http://192.168.99.101:2380"],"clientURLs":["http://192.168.99.101:2379"]}]}
2.某台机器上添加数据，其他机器上查看数据，得出的结果应该是相同的

>   
    $ curl -L http://$(docker-machine ip etcd-node-0):2379/v2/keys/message -XPUT -d value="Hello World"
    {"action":"set","node":{"key":"/message","value":"Hello World","modifiedIndex":9,"createdIndex":9}}
    $ curl -L http://$(docker-machine ip etcd-node-1):2379/v2/keys/message
    {"action":"set","node":{"key":"/message","value":"Hello World","modifiedIndex":9,"createdIndex":9}}
    $ curl -L http://$(docker-machine ip etcd-node-1):2379/v2/keys/message
    {"action":"set","node":{"key":"/message","value":"Hello World","modifiedIndex":9,"createdIndex":9}}
