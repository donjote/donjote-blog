---
title: Golang简介与环境搭建
date: 2017-07-13
categories: Golang
tags: [Golang]
---
## Golang简介
Go 是 2009 年发布的一种简单的并行开发，且跨平台的类 C 语言。由于其强大的并行性，很适合用于网络开发中
### 思想
+ Less can be more
+ 大道至简,小而蕴真
+ 让事情变得复杂很容易，让事情变得简单才难
+ 深刻的工程文化
### 优点
1. 自带gc。
2. 静态编译，编译好后，扔服务器直接运行。
3. 简单的思想，没有继承，多态，类等。
4. 丰富的库和详细的开发文档。
5. 语法层支持并发，和拥有同步并发的channel类型，使并发开发变得非常方便。
6. 简洁的语法，提高开发效率，同时提高代码的阅读性和可维护性。
7. 超级简单的交叉编译，仅需更改环境变量。（花了我两天时间编译一个imagemagick到arm平台）
8. 内含完善、全面的软件工程工具。Go语言自带的命令和工具相当地强大。通过它们，我们可以很轻松地完成Go语言程序的获取、编译、测试、安装、运行、运行分析等一系列工作，这几乎涉及了开发和维护一个软件的所有环节。
### 主要特性
+ 自动垃圾回收
+ 更丰富的内置类型
+ 函数多返回值
+ 错误处理
+ 匿名函数和闭包
+ 类型和接口
+ 并发编程
+ 反射
+ 语言交互性
+ 高性能/高效开发

## 环境搭建
### 安装
```   
    $ wget https://storage.googleapis.com/golang/go1.8.3.linux-amd64.tar.gz
    $ tar -C /usr/local -xzf go1.8.3.linux-amd64.tar.gz  
```
### 环境变量
```
    $ vim /etc/profile
```
添加对应的GOROOT和GOROOT的配置环境
```
    export GOROOT=/usr/local/go
    export GOPATH=$HOME/Projects/golang
    export PATH=$PATH:$GOROOT/bin:$GOPATH/bin
```
之后，source /etc/profile 使得其配置文件有效.

## 验证
``` 
    $ go env
    GOARCH="amd64"
    GOBIN=""
    GOEXE=""
    GOHOSTARCH="amd64"
    GOHOSTOS="linux"
    GOOS="linux"
    GOPATH="/home/donjote/Projects/golang"
    GORACE=""
    GOROOT="/usr/local/go"
    GOTOOLDIR="/usr/local/go/pkg/tool/linux_amd64"
    GCCGO="gccgo"
    CC="gcc"
    GOGCCFLAGS="-fPIC -m64 -pthread -fmessage-length=0 -fdebug-prefix-map=/tmp/go-build061263866=/tmp/go-build -gno-record-gcc-switches"
    CXX="g++"
    CGO_ENABLED="1"
    PKG_CONFIG="pkg-config"
    CGO_CFLAGS="-g -O2"
    CGO_CPPFLAGS=""
    CGO_CXXFLAGS="-g -O2"
    CGO_FFLAGS="-g -O2"
    CGO_LDFLAGS="-g -O2"
```