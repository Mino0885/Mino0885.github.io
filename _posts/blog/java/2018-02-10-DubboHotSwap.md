---
layout: post
title: Dubbo在热部署环境下遇到ClassNotFoundException的问题
categories: 其他
description: Dubbo在热部署环境下遇到ClassNotFoundException的问题
keywords: Dubbo , 热部署
---
在使用Dubbo时,开启了IDEA的JRebel的热部署插件(插件作用当ide是去焦点时,自动同步项目文件)在修改了Service的代码后,发现会有一定的几率会触发ClassNotFoundException的问题.在查询了各种资料后解决
## 出现原因
- 框架选择了java的序列化,反序列化时候会加载并寻找pojo,并且调用以下代码:
- 
![](https://i.imgur.com/tQrDoGN.png)

- latestUserDefinedLoader()默认使用了tomcat的webapploader。而在热部署环境下，loader是其它的，所以加载不到

## 解决方案

 我们可以选择其他序列化的方式,也可以继承ObjectInputStream，重写resolveClass
> 注:dubbo支持的序列化有dubbo、hessian2、java、compactedjava、json、fastjson、nativejava。其中java和nativejava序列化在热部署 环境下有问题。
  从效率和压缩比角度来看：建议使用默认的hessian2，也可以自定义为dubbo和compactedjava等方式