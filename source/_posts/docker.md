---
title: docker简介
date: 2017-08-30
categories: 容器
tags: [docker]
---
## 什么是Docker

>&emsp;&emsp;Docker 是一个开源项目，诞生于 2013 年初，最初是 dotCloud 公司内部的一个业余项目。它基于 Google 公司推出的 Go 语言实现。 它基于Linux容器技术（LXC），Namespace(命名空间)，Cgroup(控制组)，UnionFS（联合文件系统）等技术。项目后来加入了 Linux 基金会，遵从了 Apache 2.0 协议，项目代码在 GitHub 上进行维护。   

> **<font color="red"> namespace（命名空间）：</font>** 命名空间是 Linux 内核一个强大的特性。每个容器都有自己单独的名字空间，运行在其中的应用都像是在独立的操作系统中运行一样。名字空间保证了容器之间彼此互不影响。docker实际上一个进程容器，它通过namespace实现了进程和进程所使用的资源的隔离。使不同的进程之间彼此不可见。我们可以把Docker容器想像成进程＋操作系统除内核之外的一套软件。

>**<font color="red"> cgroup（控制组）：</font>** 是 Linux 内核的一个特性，主要用来对共享资源进行隔离、限制、审计等。只有能控制分配到容器的资源，才能避免当多个容器同时运行时的对系统资源的竞争。控制组技术最早是由 Google 的程序员 2006 年起提出，Linux 内核自 2.6.24 开始支持。控制组可以提供对容器的内存、CPU、磁盘 IO 等资源的限制和审计管理。

>**<font color="red"> UnionFS（联合文件系统）：</font>** Union文件系统（UnionFS）是一种分层、轻量级并且高性能的文件系统，它支持对 文件系统的修改作为一次提交来一层层的叠加，同时可以将不同目录挂载到同一个虚拟文件系统下(unite several directories into a single virtual filesystem)。Union 文件系统是 Docker 镜像的基础。镜像可以通过分层来进行继承，基于基础镜像（没有父镜像），可以制作各种具体的应用镜像。另外，不同 Docker 容器就可以共享一些基础的文件系统层，同时再加上自己独有的改动层，大大提高了存储的效率。Docker 中使用的 AUFS（AnotherUnionFS）就是一种 Union FS。 AUFS 支持为每一个成员目录（类似 Git 的分支）设定只读（readonly）、读写（readwrite）和写出（whiteout-able）权限, 同时 AUFS 里有一个类似分层的概念, 对只读权限的分支可以逻辑上进行增量地修改(不影响只读部分的)。

## 快速理解Docker
>&emsp;&emsp;拿现实世界中货物的运输作类比, 为了解决各种型号规格尺寸的货物在各种运输工具上进行运输的问题,我们发明了集装箱
![集装箱](1.jpg)
>&emsp;&emsp;docker的初衷也就是将各种应用程序和他们所依赖的运行环境打包成标准的Container/image,进而发布到不同的平台上运行
![docker](2.jpg)
>&emsp;&emsp;从理论上说这一概念并不新鲜, 各种虚拟机Image也起着类似的作用
>&emsp;&emsp;Docker container和普通的虚拟机Image相比, 最大的区别是它并不包含操作系统内核.
![docker](3.jpg)
>&emsp;&emsp;普通虚拟机将整个操作系统运行在虚拟的硬件平台上, 进而提供完整的运行环境供应用程序运行, 而Docker则直接在宿主平台上加载运行应用程序. 本质上他在底层使用LXC启动一个Linux Container,通过cgroup等机制对不同的container内运行的应用程序进行隔离,权限管理和quota分配等

>&emsp;&emsp;每个container拥有自己独立的各种命名空间(亦即资源)包括:PID 进程, MNT 文件系统, NET 网络, IPC , UTS 主机名 等

## 为什么要使用Docker
>&emsp;&emsp;作为一种新兴的虚拟化方式，Docker 跟传统的虚拟化方式相比具有众多的优势。

>&emsp;&emsp;首先，Docker 容器的启动可以在秒级实现，这相比传统的虚拟机方式要快得多。 其次，Docker 对系统资源的利用率很高，一台主机上可以同时运行数千个 Docker 容器。

>&emsp;&emsp;容器除了运行其中应用外，基本不消耗额外的系统资源，使得应用的性能很高，同时系统的开销尽量小。传统虚拟机方式运行 10 个不同的应用就要起 10 个虚拟机，而Docker 只需要启动 10 个隔离的应用即可。

>&emsp;&emsp;具体说来，Docker 在如下几个方面具有较大的优势。

> - 更快速的交付和部署
&emsp;&emsp;对开发和运维（devop）人员来说，最希望的就是一次创建或配置，可以在任意地方正常运行。
&emsp;&emsp;开发者可以使用一个标准的镜像来构建一套开发容器，开发完成之后，运维人员可以直接使用这个容器来部署代码。 Docker 可以快速创建容器，快速迭代应用程序，并让整个过程全程可见，使团队中的其他成员更容易理解应用程序是如何创建和工作的。 Docker 容器很轻很快！容器的启动时间是秒级的，大量地节约开发、测试、部署的时间。
- 更高效的虚拟化
&emsp;&emsp;Docker 容器的运行不需要额外的 hypervisor 支持，它是内核级的虚拟化，因此可以实现更高的性能和效率。
- 更轻松的迁移和扩展
&emsp;&emsp;Docker 容器几乎可以在任意的平台上运行，包括物理机、虚拟机、公有云、私有云、个人电脑、服务器等。 这种兼容性可以让用户把一个应用程序从一个平台直接迁移到另外一个。
- 更简单的管理
&emsp;&emsp;使用 Docker，只需要小小的修改，就可以替代以往大量的更新工作。所有的修改都以增量的方式被分发和更新，从而实现自动化并且高效的管理。

## Docker基本概念
>- 镜像（Image）
&emsp;&emsp;Docker的镜像概念类似于虚拟机里的镜像，是一个只读的模板，一个独立的文件系统，包括运行容器所需的数据，可以用来创建新的容器。镜像可以基于Dockerfile构建，Dockerfile是一个描述文件，里面包含若干条命令，每条命令都会对基础文件系统创建新的层次结构。用户可以通过编写Dockerfile创建新的镜像，也可以直接从类似github的Docker Hub上下载镜像使用。
- 容器（Container）
&emsp;&emsp;Docker容器是由Docker镜像创建的运行实例。Docker容器类似虚拟机，可以支持的操作包括启动，停止，删除等。每个容器间是相互隔离的，但隔离的效果比不上虚拟机。容器中会运行特定的应用，包含特定应用的代码及所需的依赖文件。

>&emsp;&emsp;在Docker容器中，每个容器之间的隔离使用Linux的 CGroups 和 Namespaces技术实现的。其中 CGroups 对CPU，内存，磁盘等资源的访问限制，Namespaces 提供了环境的隔离。
- 仓库（Repository）
&emsp;&emsp;Docker仓库相当于一个 github 上的代码库。

>&emsp;&emsp;Docker 仓库是用来包含镜像的位置，Docker提供一个注册服务器（Registry）来保存多个仓库，每个仓库又可以包含多个具备不同tag的镜像。Docker运行中使用的默认仓库是 Docker Hub 公共仓库。

>&emsp;&emsp;仓库支持的操作类似 git，创建了新的镜像后，我们可以 push 提交到仓库，也可以从指定仓库 pull 拉取镜像到本地。
