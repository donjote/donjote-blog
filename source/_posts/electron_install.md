---
title: 快速搭建Electron开发环境
date: 2017-07-09
categories: 跨平台
tags: [跨平台,Electron]
---
## Nodejs安装
查看 [Nodejs安装并配置淘宝镜像](https://donjote.github.io/2017/07/07/nodejs_install_config/)

## Electron的安装
在~/.npmrc里做如下设置
```
electron_mirror="https://npm.taobao.org/mirrors/electron/"
```
用下面的命令安装
```
$ sudo npm install -g electron  
```
## 打包输出工具
为了方便最终成果输出，建议安装electron-packager工具，安装也很简单，建议以下面的命令全局安装。
```
$ sudo npm install -g electron-packager
```
