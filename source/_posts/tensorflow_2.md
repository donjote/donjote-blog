---
title: TensorFlow入门：安装
categories: 深度学习
tags: [深度学习,神经网络,TensorFlow]
---
## 基于 Docker 的安装
>首先, [安装 Docker](https://docs.docker.com/engine/installation/). 一旦 Docker 已经启动运行, 可以通过命令启动一个容器:
>   
    $ docker run -it --name tensorflow -p 8888:8888 tensorflow/tensorflow

##才云TensorFlow镜像
>在官方镜像的基础上，才云科技提供的镜像进一步整合了其他机器学习工具包以及TensorFlow可视化工具TensorBoard，使用起来可以更加方便。
>   
    $ docker run -it  --name tensorflow -p 8888:8888 -p 6006:6006 \
    cargo.caicloud.io/caicloud/tensorflow

>在这个命令中，-p 8888:8888 将容器内运行的Jupyter服务映射到本地机器，这样在浏览器中打开localhost:8888就能看到Jupyter界面。在此镜像中运行的Jupyter是一个网页版的代码编辑器，它支持创建、上传、修改和运行Python程序。
***
-p 6006:6006将容器内运行的TensorFlow可视化工具TensorBoard映射到本地机器，通过在浏览器中打开localhost:6006就可以将TensorFlow在训练时的状态、图片数据以及神经网络结构等信息全部展示出来。此镜像会将所有输出到/log目录底下的日志全部可视化。
