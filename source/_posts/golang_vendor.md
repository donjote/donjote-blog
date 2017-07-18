---
title: Golang包管理
date: 2017-07-13
categories: Golang
tags: [Golang]
---
## 介绍
>Golang并没有官方最佳管理方案，在Go的世界里存在大量的自制解决方案。go语言的包是没有中央库统一管理的，通过使用go get命令从远程代码库(github.com,goolge code 等)拉取，直接跳过中央版本库的约束，让代码的拉取直接基于源代码版本控制库，开发者间的协同直接依赖于源代码的版本控制。直接去除了库版本的概念。没有明显的包版本标识，感觉还是有点不适应，官方的建议是把外部依赖的代码全部复制到自己可控的源代码库中，进行同意管理。从而做到对依赖包的可控管理。
***
对于国内开发者来说，最好是能一个一个包来管理。遇到网络问题，可以通过国内镜像下载。在这样的情况之下gvt 就是一个不错的选择。它可以帮助我们把一个包以及依赖都彻底的拉到本地的代码库中，统一了团队协作过程中编译环境不一致的问题。

## gvt安装方法
>   
    $ go get -u github.com/FiloSottile/gvt

## gvt使用
>### 安装包
>   
    $ gvt fetch [package]
### 下载包
>   
    $ gvt restore
### 包列表
>   
    $ gvt list
### 更新指定包
>   
    $ gvt update [package]
### 删除指定包
>   
    $ gvt delete [package]
