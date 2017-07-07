---
title: 企业级 Docker Registry--harbor安装和简单使用
categories: Docker
tags: [Docker,Docker Registry]
---
>简单的说，Harbor 是一个企业级的 Docker Registry，可以实现 images 的私有存储和日志统计权限控制等功能，并支持创建多项目(Harbor 提出的概念)，基于官方 Registry V2 实现。

## 安装docker
参考官方文档
## 安装docker-compose
参考官方文档
## 搭建Harbor
### 下载
	wget https://github.com/vmware/harbor/releases/download/v1.1.2/harbor-online-installer-v1.1.2.tgz
### 解压
	tar zvxf harbor-online-installer-v1.1.2.tgz
### 修改配置
	cd harbor
	vim harbor.cfg
配置样例如下：

	## Configuration file of Harbor

	#The IP address or hostname to access admin UI and registry service.
	#DO NOT use localhost or 127.0.0.1, because Harbor needs to be accessed by external clients.
	# 指定 hostname，一般为IP，或者域名，用于登录 Web UI 界面
	hostname = 120.12.34.45

	#The protocol for accessing the UI and token/notification service, by default it is http.
	#It can be set to https if ssl is enabled on nginx.
	# URL 访问方式，SSL 需要配置 nginx
	ui_url_protocol = http

	#Email account settings for sending out password resetting emails.
	# 邮件相关信息配置，如忘记密码发送邮件
	email_server = smtp.xxxxxx.com
	email_server_port = 465
	email_username = reg@mritd.me
	email_password = xxxxxx
	email_from = docker <reg@mritd.me>
	email_ssl = true

	##The password of Harbor admin, change this before any production use.
	# 默认的 Harbor 的管理员密码，管理员用户名默认 admin
	harbor_admin_password = Harbor12345

	##By default the auth mode is db_auth, i.e. the credentials are stored in a local database.
	#Set it to ldap_auth if you want to verify a user's credentials against an LDAP server.
	# 指定 Harbor 的权限验证方式，Harbor 支持本地的 mysql 数据存储密码，同时也支持 LDAP
	auth_mode = db_auth

	#The url for an ldap endpoint.
	# 如果采用了 LDAP，此处填写 LDAP 地址
	ldap_url = ldaps://ldap.mydomain.com

	#The basedn template to look up a user in LDAP and verify the user's password.
	# LADP 验证密码的方式(我特么没用过这么高级的玩意)
	ldap_basedn = uid=%s,ou=people,dc=mydomain,dc=com

	#The password for the root user of mysql db, change this before any production use.
	# mysql 数据库 root 账户密码
	db_password = root123

	#Turn on or off the self-registration feature
	# 是否允许开放注册
	self_registration = on

	#Turn on or off the customize your certicate
	# 允许自签名证书
	customize_crt = on

	#fill in your certicate message
	# 自签名证书信息
	crt_country = CN
	crt_state = State
	crt_location = CN
	crt_organization = mritd
	crt_organizationalunit = mritd
	crt_commonname = mritd.me
	crt_email = reg.mritd.me
	#####

### 启动
	sudo ./install
### 登录
	Harbor 默认管理员用户为 admin ，密码在 harbor.cfg 中设置过，默认的是 Harbor12345 ，可直接登陆
