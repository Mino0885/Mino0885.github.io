---
layout: post
title: Java设计模式基础
categories: SE基础
description: 列举了Java Design pattern 常用的几种
keywords: Java , 设计模式
---
## 什么是设计模式
   
- 设计模式（Design pattern）是一套被反复使用、多数人知晓的、经过分类编目的、代码设计经验的总结。

## 设计模式种类

- 创建型模式：对象实例化的模式，创建型模式用于解耦对象的实例化过程
 
   > 单例模式、抽象工厂模式、建造者模式、工厂模式、原型模式.
 
- 结构型模式：把类或对象结合在一起形成一个更大的结构

   > 适配器模式、桥接模式、装饰模式、组合模式、外观模式、享元模式、代理模式.
 
- 行为型模式：类和对象如何交互，及划分责任和算法

   > 模版方法模式、命令模式、迭代器模式、观察者模式、中介者模式、备忘录模式、解释器模式、状态模式、策略模式、职责链模式(责任链模式)、访问者模式. 

----------
下面让我们详细说说其中常用的几种

## 单例模式

简单来讲,单例模式就是指某个类只能有一个实例,提供一个全局的访问点.
实现的方式就是将构造方法私有化,并且提供一个静态的全局访问点,在自我实例化后提供全局使用
- 优点:内存中只有一个实例,减少内存消耗.避免了对资源的多重占用
- 缺点:没有接口,也不能继承,尤其是与单一职责原则冲突.不应该关系外部如何实例化
- 场景:创建的对象消耗资源很大,I/O或者数据库等
- 实现方式:

  1. 懒汉式_1 

			public class Singleton {  
    		private static Singleton instance;  
    		private Singleton (){}  
  
    		public static Singleton getInstance() {  
    		if (instance == null) {  
        	instance = new Singleton();  
    		}  
    		return instance;  
    		}  
			}  

   这种方式是最简单的实现,但是最大的问题就是**线程不安全**,因为没有加锁,所以多线程情况下很可能出问题

  2. 懒汉式_2
   
			public class Singleton {  
			private static Singleton instance;  
			private Singleton (){}  
			public static synchronized Singleton getInstance() {  
			if (instance == null) {  
	     	   instance = new Singleton();  
			}  
			return instance;  
			}  
			} 

   这种方式能在多线程中运行,但是效率很低,因为加锁影响了效率

  3. 饿汉式
 
			public class Singleton {  
    			private static Singleton instance = new Singleton();  
    			private Singleton (){}  
    			public static Singleton getInstance() {  
    			return instance;  
    			}  
			}  

   这种方式通过classloder机制避免了多线程问题,但是容易产生垃圾对象

  4. 双检锁
   
			public class Singleton {  
			private volatile static Singleton singleton;  
    			private Singleton (){}  
				public static Singleton getSingleton() {  
    			if (singleton == null) {  
        			synchronized (Singleton.class) {  
        				if (singleton == null) {  
            				singleton = new Singleton();  
        			}  
        		}  
    			}  
    			return singleton;  
    			}  
				} 
   这种方式采用了双校验机制,能在多线程情况下保证安全和高性能.  

## 工厂模式

工厂方法模式定义了一个创建对象的接口，但由子类决定要实例化的类是哪一个，也就是说工厂方法模式让实例化推迟到子类
当我们需要对代码进行更改时只需要重新实现接口下的子类就可以在不更改大量代码的情况下修改功能(引用网络中的一组图片)
![](https://images2017.cnblogs.com/blog/401339/201709/401339-20170929204041684-1520979160.png)

- 优点: 扩展性高,屏蔽了类的具体实现
- 缺点:每次都会增加一个具体的类和对象实现工厂,增加了系统的复杂度.
- 场景: 日志记录器：记录可能记录到本地硬盘、系统事件、远程服务器等，用户可以选择记录日志到什么地方. 2、数据库访问，当用户不知道最后系统采用哪一类数据库，以及数据库可能有变化时. 3、设计一个连接服务器的框架，需要三个协议，"POP3"、"IMAP"、"HTTP"，可以把这三个作为产品类，共同实现一个接口
- 实现方式:
	首先创建一个接口:
		public interface Shape {
			void draw();
		}
	创建其实现类
		public class Rectangle implements Shape {
			@Override
			public void draw() {
      		System.out.println("Inside Rectangle::draw() method.");
			}
		}
	创建工厂
		public class ShapeFactory {
    
			//使用 getShape 方法获取形状类型的对象
			public Shape getShape(String shapeType){
				if(shapeType == null){
					return null;
				}        
				if(shapeType.equalsIgnoreCase("RECTANGLE")){
				return new RECTANGLE();
				} 
				return null;
				}
				}
   如此就可以得到不同的实例对象了

## 适配器模式

在我们的应用程序中我们可能需要将两个不同接口的类来进行通信，在不修改这两个的前提下我们可能会需要某个中间件来完成这个衔接的过程。这个中间件就是适配器。所谓适配器模式就是将一个类的接口，转换成客户期望的另一个接口。它可以让原本两个不兼容的接口能够无缝完成对接。

![](https://images2017.cnblogs.com/blog/401339/201709/401339-20170929205627606-1781915371.png)

- 优点:可以让没有关系的两个类一起运行,提高复用性,增加透明度
- 缺点:过多使用会使系统异常混乱,只能适配一个适配类
- 场景:需要同时使用两个类的方法的时候
- 实现:
	创建Target接口；
		public interface Target {
			//这是源类Adapteee没有的方法
			public void Request(); 
		}

	创建源类（Adaptee） ；

		public class Adaptee {

    		public void SpecificRequest(){
    		}
		}
	创建适配器类（Adapter）
		//适配器Adapter继承自Adaptee，同时又实现了目标(Target)接口。
		public class Adapter extends Adaptee implements Target {
			//目标接口要求调用Request()这个方法名，但源类Adaptee没有方法Request()
			//因此适配器补充上这个方法名
		    //但实际上Request()只是调用源类Adaptee的SpecificRequest()方法的内容
			//所以适配器只是将SpecificRequest()方法作了一层封装，封装成Target可以调用的Request()而已
			@Override
			public void Request() {
				this.SpecificRequest();
			}

		}
	测试
		public class AdapterPattern {

			public static void main(String[] args){

			Target mAdapter = new Adapter()；
			mAdapter.Request（）;

			}
		}