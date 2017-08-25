---
title: gRPC服务方法的定义
date: 2017-08-2５
categories: gRPC
tags: [gRPC,RPC]
---
## 服务定义
>向其它的RPC服务一样，GPRC的基础是服务的定义。服务定义远程调用方法的名称、传入参数和返回参数。GRPC默认使用 Protobuf描述服务
***
GRPC一共定义4种服务方法：
1、一元RPC(Unary RPCs )：这是最简单的定义，客户端发送一个请求，服务端返回一个结果   
2、服务器流RPC（Server streaming RPCs）：客户端发送一个请求，服务端返回一个流给客户端，客户从流中读取一系列消息，直到读取所有小心   
3、客户端流RPC(Client streaming RPCs )：客户端通过流向服务端发送一系列消息，然后等待服务端读取完数据并返回处理结果   
4、双向流RPC(Bidirectional streaming RPCs)：客户端和服务端都可以独立向对方发送或接受一系列的消息。客户端和服务端读写的顺序是任意。   
***
以上的服务方法定义在proto文件，如下:   
>
        syntax = "proto3";
>
        option java_multiple_files = true;
        option java_package = "io.github.donjote.hello";
        option java_outer_classname = "HelloProto";
>
        service Hello {
        // A Unary RPC.
        rpc simpleRpc(Simple) returns (SimpleFeature) {}
>
        // A server-to-client streaming RPC.
        rpc server2ClientRpc(SimpleList) returns (stream SimpleFeature) {}
>
        // A client-to-server streaming RPC.
        rpc client2ServerRpc(stream Simple) returns (SimpleSummary) {}
>
        // A Bidirectional streaming RPC.
        rpc bindirectionalStreamRpc(stream Simple) returns (stream Simple) {}
      }
>
      message Simple {
        int32 num = 1;
        string name = 2;
      }
>
      message SimpleList {
        repeated Simple simpleList = 1;
      }
>
      message SimpleFeature {
        string name = 1;
        Simple location = 2;
      }
>
      message SimpleSummary {
        int32 feature_count = 2;
      }
>
      // 测试类
      message SimpleFeatureDatabase {
        repeated SimpleFeature feature = 1;
      }

## 同步RPC和异步RPC
>GRPC 同时支持同步RPC和异步RPC。
同步RPC调用服务方法只支持流RPC（Server streaming RPCs）和一元RPC(Unary RPCs )。异步RPC调用服务方法支持4种方法。
