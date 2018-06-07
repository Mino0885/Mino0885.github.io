---
layout: post
title: Swift中的String操作
categories: Swift
description: 简单介绍Swift中的String操作
keywords: Swift, String
---
## 锁的内存意义

- 锁可以让临界区互斥执行，还可以让释放锁的线程向同一个锁的线程发送消息
- 锁的释放要遵循Happens-before原则（锁规则：解锁必然发生在随后的加锁之前）
- 锁在Java中的具体表现是 Synchronized 和 Lock
## 需要了解的概念

 1. 临界区
 > 临界区指的是一个访问共用资源（例如：共用设备或是共用存储器）的程序片段，而这些共用资源又无法同时被多个线程访问的特性。当有线程进入临界区段时，其他线程或是进程必须等待（例如：bounded waiting 等待法），有一些同步的机制必须在临界区段的进入点与离开点实现，以确保这些共用资源是被互斥获得使用

 2. 互斥量
 > 互斥量是一个可以处于两态之一的变量：解锁和加锁。这样，只需要一个二进制位表示它，不过实际上，常常使用一个整型量，0表示解锁，而其他所有的值则表示加锁。互斥量使用两个过程。当一个线程（或进程）需要访问临界区时，它调用mutex_lock。如果该互斥量当前是解锁的（即临界区可用），此调用成功，调用线程可以自由进入该临界区。
 另一方面，如果该互斥量已经加锁，调用线程被阻塞，直到在临界区中的线程完成并调用mutex_unlock。如果多个线程被阻塞在该互斥量上，将随机选择一个线程并允许它获得锁

## 锁的种类

 自旋锁、自旋锁的其他种类、阻塞锁、可重入锁、读写锁、互斥锁、悲观锁、乐观锁、公平锁、可重入锁等等
 1. 可重入锁
 如果锁具备重入性,则称之为可重入锁.Synchronized就是可重入锁
 比如:
 > 当一个线程执行到method1 的synchronized方法时，而在method1中会调用另外一个synchronized方法method2，此时该线程不必重新去申请锁，而是可以直接执行方法method2
 2. 读写锁
 读写锁将对资源的访问分为了两个锁,如他的名字一样,一个是读锁,一个是写锁,整数因为这种锁的存在才能保证我们读写文件时候,不会发生冲突
 ReadWriteLock就是读写锁,是一个接口,ReentrantReadWriteLock实现了这个接口,可以通过readLock()获取读锁,通过writeLock()获取写锁.

 3. 可中断锁
 可中断锁,即为可以中断的锁,** Lock是可中断的锁,而Synchronized是不可中断的锁 ** 如果某一线程A正在执行锁中的代码，另一线程B正在等待获取该锁，可能由于等待时间过长，线程B不想等待了，想先处理其他事情，我们可以让它中断自己或者在别的线程中中断它，这种就是可中断锁。
 Lock接口中的lockInterruptibly()方法就体现了Lock的可中断性。

 4. 公平锁
 公平锁会按照请求锁的顺序来获取锁,同时会有多个线程等待这个锁,当这个锁被释放后,等待最久的线程会获得该锁
 注意:线程会默认的主动去尝试获取锁,所以最后执行顺序并不会按照先后顺序执行

## Synchronized
 Synchronized是java中的一个关键字.有大约如下四种使用方法.
 - 同步代码块1:
 注意:括号中的m是变量.
		public int synMethod(int m){
    		synchronized(m) {
     		//...
    		}
		}
 - 同步方法
		public synchronized void synMethod() {
   			//...
		}
 - 同步代码块2:
 注意括号中的是一个对象
		public void test() {
			synchronized (this) {
      		//...
			}
		}
 - Synchronized后面跟类
 synchronized后面括号里是类，如果线程进入，则线程在该类中所有操作不能进行，包括静态变量和静态方法，对于含有静态方法和静态变量的代码块的同步，通常使用这种方式

## Lock
 首先毋庸置疑,Lock是一个接口,而其中有如下代码

		public interface Lock {
			void lockInterruptibly() throws InterruptedException;
			boolean tryLock();
			boolean tryLock(long time, TimeUnit unit) throws InterruptedException;
			void unlock();
			Condition newCondition();
		}

 - lock：用来获取锁，如果锁被其他线程获取，处于等待状态。如果采用Lock，必须主动去释放锁，并且在发生异常时，不会自动释放锁。** 因此一般来 说，使用Lock必须在try{}catch{}块中进行，并且将释放锁的操作放在finally块中进行，以保证锁一定被被释放，防止死锁的发生**。


 - lockInterruptibly：通过这个方法去获取锁时，如果线程正在等待获取锁，则这个线程能够响应中断，即中断线程的等待状态。


 - tryLock：tryLock方法是有返回值的，它表示用来尝试获取锁，如果获取成功，则返回true，如果获取失败（即锁已被其他线程获取），则返回false，也就说这个方法无论如何都会立即返回。在拿不到锁时不会一直在那等待。


 - tryLock（long，TimeUnit）：与tryLock类似，只不过是有等待时间，在等待时间内获取到锁返回true，超时返回false。


 - unlock：** 释放锁，一定要在finally块中释放 **

## 两种锁的比较
 - Lock是一个接口，而synchronized是Java中的关键字，synchronized是内置的语言实现；
 - synchronized在发生异常时，会自动释放线程占有的锁，因此不会导致死锁现象发生；而Lock在发生异常时，如果没有主动通过unLock()去释放锁，则很可能造成死锁现象，因此使用Lock时需要在finally块中释放锁；
 - Lock可以让等待锁的线程响应中断，而synchronized却不行，使用synchronized时，等待的线程会一直等待下去，不能够响应中断；
 - 通过Lock可以知道有没有成功获取锁，而synchronized却无法办到。
 - Lock可以提高多个线程进行读操作的效率。（可以通过readwritelock实现读写分离）
 - 性能上来说，在资源竞争不激烈的情形下，Lock性能稍微比synchronized差点（编译程序通常会尽可能的进行优化synchronized）。但是当同步非常激烈的时候，synchronized的性能一下子能下降好几十倍。而ReentrantLock确还能维持常态。

----------
参考自:[掘金](https://juejin.im/post/5a43ad786fb9a0450909cb5f)
