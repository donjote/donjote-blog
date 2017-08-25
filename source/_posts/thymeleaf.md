---
title: thymeleaf 使用
date: 2017-08-25
categories: Java
tags: [spring boot]
---
## thymeleaf介绍
>简单说， Thymeleaf 是一个跟 Velocity、FreeMarker 类似的模板引擎，它可以完全替代 JSP 。相较与其他的模板引擎，它有如下三个极吸引人的特点：
- Thymeleaf 在有网络和无网络的环境下皆可运行，即它可以让美工在浏览器查看页面的静态效果，也可以让程序员在服务器查看带数据的动态页面效果。这是由于它支持 html 原型，然后在 html 标签里增加额外的属性来达到模板+数据的展示方式。浏览器解释 html 时会忽略未定义的标签属性，所以 thymeleaf 的模板可以静态地运行；当有数据返回到页面时，Thymeleaf 标签会动态地替换掉静态内容，使页面动态显示。
- Thymeleaf 开箱即用的特性。它提供标准和spring标准两种方言，可以直接套用模板实现JSTL、 OGNL表达式效果，避免每天套模板、该jstl、改标签的困扰。同时也可以扩展和创建自定义的方言。
- Thymeleaf 提供spring标准方言和一个与 SpringMVC 完美集成的可选模块，可以快速的实现表单绑定、属性编辑器、国际化等功能。

## 标准表达式语法
>分为四类：
1. 变量表达式
2. 选择或星号表达式
3. 文字国际化表达式
4. URL表达式

### 变量表达式
>变量表达式即OGNL表达式或Spring EL表达式(在Spring术语中也叫model attributes)。如下所示：
>
    ${session.user.name}
它们将以HTML标签的一个属性来表示：
>
    <span th:text="${book.author.name}"></span>
    <li th:each="book : ${books}"></li>

### 选择(星号)表达式
>选择表达式很像变量表达式，不过它们用一个预先选择的对象来代替上下文变量容器(map)来执行，如下：
>
    * {customer.name}
> 被指定的object由th:object属性定义：
>
    <div th:object="${book}">  
      ...  
      <span th:text="* {title}">...</span>  
      ...  
    </div>  

### 文字国际化表达式
>文字国际化表达式允许我们从一个外部文件获取区域文字信息(.properties)，用Key索引Value，还可以提供一组参数(可选).
>
    #{main.title}  
    #{message.entrycreated(${entryId})}  
可以在模板文件中找到这样的表达式代码：
>
    <table>  
      ...  
      <th th:text="#{header.address.city}">...</th>  
      <th th:text="#{header.address.country}">...</th>  
      ...  
    </table>  

### URL表达式
> URL表达式指的是把一个有用的上下文或回话信息添加到URL，这个过程经常被叫做URL重写。
>
    @{/order/list}
URL还可以设置参数：
>
    @{/order/details(id=${orderId})}
相对路径：
>
    @{../documents/report}
让我们看这些表达式：
>
    <form th:action="@{/createOrder}">  
    <a href="main.html" th:href="@{/main}">

### 变量表达式和星号表达有什么区别吗？
>如果不考虑上下文的情况下，两者没有区别；星号语法评估在选定对象上表达，而不是整个上下文
什么是选定对象？就是父标签的值，如下：
>
    <div th:object="${session.user}">
      <p>Name: <span th:text="* {firstName}">Sebastian</span>.</p>
      <p>Surname: <span th:text="* {lastName}">Pepper</span>.</p>
      <p>Nationality: <span th:text="* {nationality}">Saturn</span>.</p>
    </div>
这是完全等价于：
>
    <div th:object="${session.user}">
        <p>Name: <span th:text="${session.user.firstName}">Sebastian</span>.</p>
        <p>Surname: <span th:text="${session.user.lastName}">Pepper</span>.</p>
        <p>Nationality: <span th:text="${session.user.nationality}">Saturn</span>.</p>
    </div>
当然，美元符号和星号语法可以混合使用：
>
    <div th:object="${session.user}">
        <p>Name: <span th:text="* {firstName}">Sebastian</span>.</p>
        <p>Surname: <span th:text="${session.user.lastName}">Pepper</span>.</p>
        <p>Nationality: <span th:text="* {nationality}">Saturn</span>.</p>
    </div>

## 表达式支持的语法
>### 字面（Literals）
> - 文本文字（Text literals）: 'one text', 'Another one!',…
- 数字文本（Number literals）: 0, 34, 3.0, 12.3,…
- 布尔文本（Boolean literals）: true, false
- 空（Null literal）: null
- 文字标记（Literal tokens）: one, sometext, main,…
### 文本操作（Text operations）
 - 字符串连接(String concatenation): +
- 文本替换（Literal substitutions）: |The name is ${name}|
### 算术运算（Arithmetic operations）
- 二元运算符（Binary operators）: +, -, * , /, %
- 减号（单目运算符）Minus sign (unary operator): -
### 布尔操作（Boolean operations）
- 二元运算符（Binary operators）:and, or
- 布尔否定（一元运算符）Boolean negation (unary operator):!, not
### 比较和等价(Comparisons and equality)
- 比较（Comparators）: >, <, >=, <= (gt, lt, ge, le)
- 等值运算符（Equality operators）:==, != (eq, ne)
### 条件运算符（Conditional operators）
> - If-then: (if) ? (then)
- If-then-else: (if) ? (then) : (else)
- Default: (value) ?: (defaultvalue)
### 所有这些特征可以被组合并嵌套：
>
      'User is of type ' + (${user.isAdmin()} ? 'Administrator' : (${user.type} ?: 'Unknown'))

## 常用th标签都有那些？
> 
关键字	| 功能介绍 | 案例
------|----- |-----
th:id | 替换id | &lt;input th:id="'xxx' + ${collect.id}"/>
th:text | 文本替换 |  &lt;p th:text="${collect.description}">description</p>
th:utext | 支持html的文本替换	|  &lt;p th:utext="${htmlcontent}">conten</p>
th:object | 替换对象 |	 &lt;div th:object="${session.user}">
th:value	| 属性赋值 |	 &lt;input th:value="${user.name}" />
th:with |	变量赋值运算 |	 &lt;div th:with="isEven=${prodStat.count}%2==0"></div>
th:style |	设置样式	| th:style="'display:' + @{(${sitrue} ? 'none' : 'inline-block')} + ''"
th:onclick | 点击事件 |	th:onclick="'getCollect()'"
th:each	| 属性赋值 |	tr th:each="user,userStat:${users}">
th:if	| 判断条件 |	 &lt;a th:if="${userId == collect.userId}" >
th:unless |	和th:if判断相反	|  &lt;a th:href="@{/login}" th:unless=${session.user != null}>Login</a>
th:href |	链接地址 |	 &lt;a th:href="@{/login}" th:unless=${session.user != null}>Login</a> />
th:switch |	多路选择 配合th:case 使用 |	 &lt;div th:switch="${user.role}">
th:case |	th:switch的一个分支	|  &lt;p th:case="'admin'">User is an administrator</p>
th:fragment |	布局标签，定义一个代码片段，方便其它地方引用 |	 &lt;div th:fragment="alert">
th:include | 布局标签，替换内容到引入的文件 |	 &lt;head th:include="layout :: htmlhead" th:with="title='xx'"></head> />
th:replace |	布局标签，替换整个标签到引入的文件 |	 &lt;div th:replace="fragments/header :: title"></div>
th:selected |	selected选择框 选中 |	th:selected="(${xxx.id} == ${configObj.dd})"
th:src |	图片类地址引入 |	 &lt;img class="img-responsive" alt="App Logo" th:src="@{/img/logo.png}" />
th:inline |	定义js脚本可以使用变量 |	 &lt;script type="text/javascript" th:inline="javascript">
th:action |	表单提交的地址	|  &lt;form action="subscribe.html" th:action="@{/subscribe}">
th:remove |	删除某个属性 |	 &lt;tr th:remove="all"> 1.all:删除包含标签和所有的孩子。
th:attr |	设置标签属性，多个属性可以用逗号分隔 |	比如 th:attr="src=@{/image/aa.jpg},title=#{logo}"，此标签不太优雅，一般用的比较少。
***
> 还有非常多的标签，这里只列出最常用的几个,由于一个标签内可以包含多个th:x属性，其生效的优先级顺序为:
include,each,if/unless/switch/case,with,attr/attrprepend/attrappend,value/href,src ,etc,text/utext,fragment,remove。
