---
title: 幂等性
categories: 架构
tags: [架构,分布式架构]
---
## 幂等性定义
### 数学定义
>在数学里，幂等有两种主要的定义：
+ 在某二元运算下，幂等元素是指被自己重复运算(或对于函数是为复合)的结果等于它自己的元素。例如，乘法下唯一两个幂等实数为0和1。 即 s * s = s
+ 某一元运算为幂等的时，其作用在任一元素两次后会和其作用一次的结果相同。例如，高斯符号便是幂等的，即f(f(x)) = f(x)。

### HTTP规范的定义
> 在HTTP/1.1规范中幂等性的定义是：
***
Methods can also have the property of "idempotence" in that (aside from error or expiration issues) the side-effects of N > 0 identical requests is the same as for a single request.
***
从定义上看，HTTP方法的幂等性是指一次和多次请求某一个资源应该具有同样的副作用。幂等性属于语义范畴，正如编译器只能帮助检查语法错误一样，HTTP规范也没有办法通过消息格式等语法手段来定义它，这可能是它不太受到重视的原因之一。但实际上，幂等性是分布式系统设计中十分重要的概念，而HTTP的分布式本质也决定了它在HTTP中具有重要地位。

## HTTP的幂等性
>HTTP协议本身是一种面向资源的应用层协议，但对HTTP协议的使用实际上存在着两种不同的方式：一种是RESTful的，它把HTTP当成应用层协议，比较忠实地遵守了HTTP协议的各种规定；另一种是SOA的，它并没有完全把HTTP当成应用层协议，而是把HTTP协议作为了传输层协议，然后在HTTP之上建立了自己的应用层协议。本文所讨论的HTTP幂等性主要针对RESTful风格的，不过正如上一节所看到的那样，幂等性并不属于特定的协议，它是分布式系统的一种特性；所以，不论是SOA还是RESTful的Web API设计都应该考虑幂等性。下面将介绍HTTP GET、DELETE、PUT、POST四种主要方法的语义和幂等性。
***
HTTP GET方法用于获取资源，不应有副作用，所以是幂等的。
***
HTTP DELETE方法用于删除资源，有副作用，但它应该满足幂等性。
***
比较容易混淆的是HTTP POST和PUT。POST和PUT的区别容易被简单地误认为“POST表示创建资源，PUT表示更新资源”；而实际上，二者均可用于创建资源，更为本质的差别是在幂等性方面。在HTTP规范中对POST和PUT是这样定义的：
***
The POST method is used to request that the origin server accept the entity enclosed in the request as a new subordinate of the resource identified by the Request-URI in the Request-Line ...... If a resource has been created on the origin server, the response SHOULD be 201 (Created) and contain an entity which describes the status of the request and refers to the new resource, and a Location header.
***
The PUT method requests that the enclosed entity be stored under the supplied Request-URI. If the Request-URI refers to an already existing resource, the enclosed entity SHOULD be considered as a modified version of the one residing on the origin server. If the Request-URI does not point to an existing resource, and that URI is capable of being defined as a new resource by the requesting user agent, the origin server can create the resource with that URI.
***
POST所对应的URI并非创建的资源本身，而是资源的接收者。两次相同的POST请求会在服务器端创建两份资源，它们具有不同的URI；所以，POST方法不具备幂等性。而PUT所对应的URI是要创建或更新的资源本身。对同一URI进行多次PUT的副作用和一次PUT是相同的；因此，PUT方法具有幂等性。

## 幂等的实现方案
### 查询操作
>查询一次和查询多次，在数据不变的情况下，查询结果是一样的。select是天然的幂等操作

### 删除操作
>删除操作也是幂等的，删除一次和多次删除都是把数据删除。(注意可能返回结果不一样，删除的数据不存在，返回0，删除的数据多条，返回结果多个)

### 唯一索引，防止新增脏数据
>比如：支付宝的资金账户，支付宝也有用户账户，每个用户只能有一个资金账户，怎么防止给用户创建资金账户多个，那么给资金账户表中的用户ID加唯一索引，所以一个用户新增成功一个资金账户记录
***
**要点：
唯一索引或唯一组合索引来防止新增数据存在脏数据（当表存在唯一索引，并发时新增报错时，再查询一次就可以了，数据应该已经存在了，返回结果即可）**

### token机制，防止页面重复提交
>#### 业务要求：
页面的数据只能被点击提交一次
#### 发生原因：
由于重复点击或者网络重发，或者nginx重发等情况会导致数据被重复提交
#### 解决办法：
集群环境：采用token加redis（redis单线程的，处理需要排队）
单JVM环境：采用token加redis或token加jvm内存
#### 处理流程：
1. 数据提交前要向服务的申请token，token放到redis或jvm内存，token有效时间
2. 提交后后台校验token，同时删除token，生成新的token返回
#### token特点：
要申请，一次有效性，可以限流
***
**注意：
redis要用删除操作来判断token，删除成功代表token校验通过，如果用select+delete来校验token，存在并发问题，不建议使用**

### 悲观锁
>获取数据的时候加锁获取
select * from table_xxx where id='xxx' for update;
注意：id字段一定是主键或者唯一索引，不然是锁表，会死人的
悲观锁使用时一般伴随事务一起使用，数据锁定时间可能会很长，根据实际情况选用

### 乐观锁
>乐观锁只是在更新数据那一刻锁表，其他时间不锁表，所以相对于悲观锁，效率更高。
乐观锁的实现方式多种多样可以通过version或者其他状态条件：
1. 通过版本号实现
update table_xxx set name=#name#,version=version+1 where version=#version#
如下图(来自网上)：
![乐观锁](1.png)
2. 通过条件限制
update table_xxx set avai_amount=avai_amount-#subAmount# where avai_amount-#subAmount# >= 0
要求：quality-#subQuality# >= ，这个情景适合不用版本号，只更新是做数据安全校验，适合库存模型，扣份额和回滚份额，性能更高
***
**注意：乐观锁的更新操作，最好用主键或者唯一索引来更新,这样是行锁，否则更新时会锁表，上面两个sql改成下面的两个更好
update table_xxx set name=#name#,version=version+1 where id=#id# and version=#version#
update table_xxx set avai_amount=avai_amount-#subAmount# where id=#id# and avai_amount-#subAmount# >= 0**

### 分布式锁
>还是拿插入数据的例子，如果是分布是系统，构建全局唯一索引比较困难，例如唯一性的字段没法确定，这时候可以引入分布式锁，通过第三方的系统(redis或zookeeper)，在业务系统插入数据或者更新数据，获取分布式锁，然后做操作，之后释放锁，这样其实是把多线程并发的锁的思路，引入多多个系统，也就是分布式系统中得解决思路。
***
**要点：某个长流程处理过程要求不能并发执行，可以在流程执行之前根据某个标志(用户ID+后缀等)获取分布式锁，其他流程执行时获取锁就会失败，也就是同一时间该流程只能有一个能执行成功，执行完成后，释放分布式锁(分布式锁要第三方系统提供)**

### select + insert
>并发不高的后台系统，或者一些任务JOB，为了支持幂等，支持重复执行，简单的处理方法是，先查询下一些关键数据，判断是否已经执行过，在进行业务处理，就可以了
***
**注意：核心高并发流程不要用这种方法**

### 状态机幂等
>在设计单据相关的业务，或者是任务相关的业务，肯定会涉及到状态机(状态变更图)，就是业务单据上面有个状态，状态在不同的情况下会发生变更，一般情况下存在有限状态机，这时候，如果状态机已经处于下一个状态，这时候来了一个上一个状态的变更，理论上是不能够变更的，这样的话，保证了有限状态机的幂等。

### 对外提供接口的api如何保证幂等
>如银联提供的付款接口：需要接入商户提交付款请求时附带：source来源，seq序列号
source+seq在数据库里面做唯一索引，防止多次付款，(并发时，只能处理一个请求)
***
**重点：
对外提供接口为了支持幂等调用，接口有两个字段必须传，一个是来源source，一个是来源方序列号seq，这个两个字段在提供方系统里面做联合唯一索引，这样当第三方调用时，先在本方系统里面查询一下，是否已经处理过，返回相应处理结果；没有处理过，进行相应处理，返回结果。注意，为了幂等友好，一定要先查询一下，是否处理过该笔业务，不查询直接插入业务系统，会报错，但实际已经处理了。**

## 总结：
>幂等性应该是合格程序员的一个基因，在设计系统时，是首要考虑的问题，尤其是在像支付宝，银行，互联网金融公司等涉及的都是钱的系统，既要高效，数据也要准确，所以不能出现多扣款，多打款等问题，这样会很难处理，用户体验也不好
