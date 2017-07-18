---
title: Yarn介绍
date: 2017-07-10
categories: Nodejs
tags: [Nodejs,Yarn]
---
## Yarn介紹
>Facebook发布的新一代包管理工具，旨在解决以往使用npm作为包管理会遇到的一些问题。从其官方介绍可以看到其重点强调的3个点：快、可靠、安全。

## Yarn特性
> ### 离线模式
以前安装过的包可以在没有任何互联网连接的情况下重新安装。
### 确定性
不管安装顺序如何，相同的依赖关系将在每台机器上以相同的方式安装。
### 网络性能
Yarn 有效地对请求进行排队，并避免 request waterfalls， 以便最大限度地利用网络。
### 多个 Registries
支持从 npm 或 Bower 安装包，并保持安装包的工作流程相同。
### 网络恢复
单个请求失败不会导致安装失败，而会重试请求。
### 扁平模式
将不兼容版本的依赖项解析为单个版本，以避免重复下载。

## 安装方法
>     
    $ sudo npm i -g yarn

## 设置淘宝镜像
>    
    $ yarn config set registry https://registry.npm.taobao.org --global
    $ yarn config set disturl https://npm.taobao.org/dist --global


## 用法
> ### 初始化一个新的项目
      $ yarn init
  ### 添加一个依赖包
      $ yarn add [package]
      $ yarn add [package]@[version]
      $ yarn add [package]@[tag]
  ### 更新一个依赖包
      $ yarn upgrade [package]
      $ yarn upgrade [package]@[version]
      $ yarn upgrade [package]@[tag]
  ### 移除一个依赖包
      $ yarn remove [package]
  ### 安装项目所有的依赖包
      $ yarn
      或
      $ yarn install
