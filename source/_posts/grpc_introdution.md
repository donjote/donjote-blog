---
title: gRPC入门简介
date: 2017-08-23
categories: gRPC
tags: [gRPC,RPC]
---
## 简介
> [gRPC](https://grpc.io/)是Go实现的：一个高性能，开源，将移动和HTTP/2放在首位通用的RPC框架， 有关详细信息，请参阅[gRPC快速入门指南](https://grpc.io/docs/)。
### gRPC概念图
>![gRPC概念图](1.png)

## gRPC特性
### 基于HTTP/2协议标准
> #### 什么是HTTP/2协议
HTTP 2.0即超文本传输协议 2.0，是下一代HTTP协议（基于二进制的传输协议）。是由互联网工程任务组（IETF）的Bis (httpbis)工作小组进行开发。
#### HTTP/2的优点
+ http2减少了网络往返传输的数量，并且用多路复用和快速丢弃不需要的流的办法来完全避免head of line blocking(线头阻塞)的困扰，降低延迟并提高安全性。
+ 支持大量并行流，所以即使网站的数据分发在各处也不是问题。
+ 合理利用流的优先级，可以让客户端尽可能优先收到更重要的数据。

### gRPC基于强大的IDL(Interface description language)
> gRPC基于ProtoBuf(Protocol Buffers)定义接口规范。
#### ProtoBuf是什么？
Protocol Buffers 是google提供的一种轻便、高效、简单的数据存储语言，可以用于结构化、序列化数据。
#### 为什么要使用ProtoBuf？
+ 适合应用场景：它很适合做数据存储或 RPC 数据交换格式。可用于通讯协议、数据存储等领域的语言无关、平台无关、可扩展的序列化数据结构。
+ 支持语言众多（提供了完善的API）:Proto2提供了 C++、Java、Python 三种语言的 API。目前语言版本Proto3提供了更多的语言支持,包括 C++ 、C# 、GO 、JAVA、PYTHON。
+ 易学易懂：protoBuf语法非常简单，掌握非常容易，便于读写。

### gRPC支持众多开发语言
>GRPC目前支持的开发语言已达到了10种：C, C++, Java, Go, Node.js, Python, Ruby, Objective-C, PHP and C#。并且GRPC框架已在GitHub上开源。
 GitHub地址：https://github.com/grpc
 JAVA GitHub地址：https://github.com/grpc/grpc-java

## 为什么使用gRPC
> + 它使用HTTP2协议，可复用链接，更充分的利用底层TCP传输协议，并以数据流的方式传输，比其他基于HTTP1的传输速率更高。
+ 它基于Proto Buffer语言,对传输数据进行压缩、系列化和结构化，易于客户端与服务端数据的读写操作，并使数据量传输变得更小、传输效率更高。
+ 基于以上及其他特性，使得基于GRPC的客户端和服务端更高效的利用流和链接，从而有助于节省宽带流量、降低链接次数、提高CUP使用效率和电池的使用寿命。
