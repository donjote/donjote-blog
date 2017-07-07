---
title: Nodejs安装并配置淘宝镜像
categories: Nodejs
tags: [Nodejs,npm镜像]
---
## 安装Node.js
>安装 Node.js 方式多种多样，最简单的方式是在[Node.js 官网](https://nodejs.org/en/) 下载可执行程序直接安装即可。
+ 对于 Mac，可以使用 [Homebrew](http://brew.sh/) 进行安装：
      brew install node
更多安装方式可参考 [Node.js 官方信息](https://nodejs.org/en/download/)
+ 安装完成后，可以使用以下命令检测是否安装成功:
      $ node -v
      v6.11.0
      $ npm -v
      3.10.10

## 配置Node.js
>使用淘宝的 npm 镜像
+ 通过config命令
      $ npm config set registry https://registry.npm.taobao.org   
      $ npm info underscore （如果上面配置正确这个命令会有字符串response）
+ 命令行指定
      $ npm --registry https://registry.npm.taobao.org info underscore    
+ 编辑 ~/.npmrc 加入下面内容
      registry = https://registry.npm.taobao.org
