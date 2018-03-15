---
layout: post
title: Collection集合
categories: SE基础
description: Collection详解
keywords: java,Collection,集合
---
 本文主要讲解一些关于Collection集合的知识和相关问题

----------
![](https://i.imgur.com/2zvOEb2.png)
这是我早些时候总结的一个关于Collection的xmind文件,左上角为Collection的大致接口继承结构(可缩放页面查看)
## Collection是什么
Collection又称为集合,与Map一样是Java中的两种容器.是用来存储其他对象的容器.
## Collection的特点
- 集合的长度可变
- 集合不可以存储基本数据类型(可以存储成其封装好的对象)

## Collection的两个子接口
1. List 
   线性表,有序,允许重复
2. Set
   规则集,不一定有序(无序),不允许重复

##List
- ArrayList(常用)
   底层数据结构:数组结构
   特点:查询快,增删慢
   安全与效率:线程不安全,但是效率较高
- Vector
   底层数据结构:数组结构
   特点:查询快,增删慢
   安全与效率:线程安全,效率较低
- LinkedList
   底层数据结构:链表结构
   特点:查询慢,增删快
   安全与效率:线程不安全,效率较高

##Set
Set集合不常用,最常见的使用场景是用来去除重复的元素
- HashSet
   底层数据结构:哈希表
   特点:可以保证元素的唯一性(JavaBean需要自己重写hashCode()和equals()方法)
- LinkedHashSet
   底层数据结构:链表结构+哈希表
   特点:可以保证存取有序,并保证唯一(链表保证了存取相对有序,并且哈希表保证了元素唯一)

## Collection和Collections的区别
Collection是一个集合接口,而Collections是一个包装类,他在java.util包下,有很多关于集合的静态方法,是一个工具类 
   