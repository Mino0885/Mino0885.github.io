---
layout: post
title: IDEA工具使用中遇到的问题-Mybatis找不到Mapper.xml
categories: IDEA使用问题
description: IDEA工具使用中发现Mybatis的配置文件Mapper.xml无法正常编译,以下为解决方案
keywords: IDEA, Mybatis
---
闲暇之余想自己写个小项目来实践最近吸收到的技术,准备采用SSM框架来操作,却发现MYBATIS反复出现以下错误

![出现的错误](https://i.imgur.com/eQ4VOHM.png)
 
是建立了一个单独的Mybatis工程来实验:

![项目结构](https://i.imgur.com/T5kUB7K.png)

在编译之后发现问题:编译后的文件中Mapper文件夹下并没有出现.xml文件

![输出目录](https://i.imgur.com/mPvvuJW.png)

----------

#### 无法编译的原因

这个问题主要是因为IDEA工具不同于其他IDE工具;IDEA 编译后默认会把 resources 下的文件放到 target 的 classpath 下，但是 src 下的只有.java 文件编译生成.class 文件放入 classpath 下，其他文件会忽略的。所以我们编译后的mapper目录中并没有.xml文件

#### 关于解决方案
- 解决方案1:在resource目录下添加一个同名文件夹,将.xml文件放入此目录.编译后正常.

 ![解决方案1](https://i.imgur.com/fyk2EQs.png)

- 解决方案2:在pom.xml中配置如下代码(适用于Maven项目)

![](https://i.imgur.com/ItSjudr.png)

----------
编译后一切正常

![](https://i.imgur.com/KtaJTj6.png)


