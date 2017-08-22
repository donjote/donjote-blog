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
 Yarn命令列表

 命令  | 操作 | 参数 | 标签
------|-----|------|-----
yarn add  | 添加依赖包  | 包名  | –dev/-D
yarn bin  | 显示yarn安装目录  | 无  | 无
yarn cache  | 显示缓存  | 列出缓存包：ls，打出缓存目录路径：dir，清除缓存：clean  | 无
yarn check  | 检查包  |   |
yarn config	 | 配置  | 设置：set <key> <value>， 删除：delete， 列出：list	 | [-g或--global]
yarn generate-lock-entry | 生成锁定文件	 | 无	| 无
yarn global | 全局安装依赖包 | yarn global <add/bin/ls/remove/upgrade> [–prefix]	 | –prefix 包路径前缀
yarn info | 显示依赖包的信息 | 包名 | –json：json格式显示结果
yarn init | 互动式创建/更新package.json文件 | 无 | –yes/-y：以默认值生成package.json文件
yarn install | 安装所有依赖包 |  | –flat：只安装一个版本；–force：强制重新下载安装；–har：输出安装时网络性能日志；–no-lockfile：不生成yarn.lock文件；–production：生产模式安装（不安装devDependencies中的依赖）
yarn licenses | 列出已安装依赖包的证书 | ls：证书列表；generate-disclaimer：生成免责声明 |
yarn link | 开发时链接依赖包，以便在其他项目中使用 | 包名 |
yarn login | 保存你的用户名、邮箱	 |  |
yarn logout | 删除你的用户名、邮箱 |  | 	
yarn list | 列出已安装依赖包 |  | –depth=0：列表深度，从0开始
yarn outdated | 检查过时的依赖包 | 包名 |
yarn owner | 管理拥有者 | ls/add/remove |
yarn pack | 给包的依赖打包 | –filename |
yarn publish | 将包发布到npm |  | –tag：版本标签；–access：公开（public）还是限制的（restricted）
yarn remove | 卸载包，更新package.json和yarn.lock | 包名 |
yarn run | 运行package.json中预定义的脚本	 |  | 	
yarn self-update | yarn自身更新–未实现 |  |
yarn tag | 显示包的标签 | add/rm/ls |
yarn team | 管理团队 | create/destroy/add/rm/ls |
yarn test | 测试 = yarn run test	 |  | 	
yarn unlink | 取消链接依赖包		 |  |
yarn upgrade | 升级依赖包	 |  | 	
yarn version | 管理当前项目的版本号	 | –new-version ：直接记录版本号；–no-git-tag-version：不生成git标签 |
yarn why | 分析为什么需要安装依赖包 | 包名/包目录/包目录中的文件名 | 
