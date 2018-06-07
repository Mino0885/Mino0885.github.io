---
layout: post
title: Swift中的String操作
categories: Swift
description: 简单介绍Swift中的String操作
keywords: Swift, String
---
入坑IOS开发,在此写下一些学习Swift时候的总结
### String相关操作

    //创建字符串
    var stringA = "Hello, World!"
    var myInt = 888
    //创建空字符串
    var stringC = ""
    var stringD = String()
    //在字符串中插入变量(常量)
    var stringE = "\(stringA) 拼接 \(myInt)"
    print(stringE)    //Hello, World! 拼接 888
    //字符串比较 可以直接使用 == 比较
    print(stringC==stringD)   //true
    //insert() 指定索引插入字符
    stringA.insert("h", at: stringA.endIndex)
    print(stringA)    //Hello, World!h
    //insert(contentsOf:"") 指定索引插入字符
    stringA.insert(contentsOf:"ahhah", at: stringA.endIndex)
    print(stringA)    //Hello, World!ahhah
    //remove
常用的函数:
 - isEmpty  判断是否为空
 - hasPrefix(prefix: String)  判断是否以某个字符串开头
 - hasSuffix(suffix: String)  判断是否以某个字符串结尾
 -

#### 索引
- 首尾索引使用

  在Swift中Strng是Unicode字符集组成的 ,优点就不再介绍了,有一个弊端就是不能像java 等语言一样用数字来访问具体的字符 .但是同时Swift也为我们提供了相应的字符串索引(Sting.Index).

      var str = "Hello Mino"
      print(str[str.startIndex])
      print(str[str.index(before:str.endIndex)])
   这里str.startIndex 获取到的是String 的第一个字符 而endIndex却不是一个合法的下标
- 如何计算String长度
      print(str.count)
