title: java多线程开发
author: bigcong
tags:
  - 多线程
categories: []
date: 2017-04-24 06:16:00
---
## 引
* 多线程：指程序产生了不止一个线程
* 并发与并行

  * 并发：多个CPU实例或者多台机器同时执行同一段逻辑代码
  * 并行：通过cpu的调度算法，让用户看上去同时执行，实际上从cpu操作层面并不是真正的同时，并发场景往往有公用的资源，那么针对TPS或者QPS来反应这个系统的处理能力
  

* 线程安全：常常我们描绘一段代码，指在并发的情况下，该代码经过多线程的使用，线程的调度顺序不影响任何结果。这个时候我们指关注系统的cpu，cpu是不是够用
* 同步：java中的同步是指通过人为控制和调度，保持共享资源的多线程成为线程安全，来保证结果的正确性，synchronized关键字，在保持结果的同时，提高的性能

## 线程状态
### 状态列表
* 1. NEW
* 2. RUNNABLE
* 3. BLOCKED
* 4. WAITING
* 5. TIMED_WATITING
* 6. TERMINATED

状态流转： 
![状态流转](http://upload-images.jianshu.io/upload_images/1689841-383f7101e6588094.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240&_=5479442 "状态流转")
* 在线程的Running 可能遇会遇到阻塞(Blocked)情况

  * 1. 调用join()和sleep方法结束或者被打断，join中断，IO完成都会回到Runnable状态，等待JVM调用
  * 2.  调用wait（），该线程处在等待池（wait blocked pool）状态，直到notify／notifyall，线程被唤醒被锁定到池当中，释放同步锁使线程回到可运行状态
  * 3. 对于running状态的线程加同步锁，使其进入blocked，同步锁被释放进入可运用的状态
  
  
## 多线程的实现方法
* java的实现多线程的方法有两种，一种继承thread类，一种实现runnable接口，在开发实践当中，以实现runnable接口为主，因为实现runnable接口比继承thread类有如下优势：

1. >可以比较由于java的单继承而带来的局限性

2. >增加程序的健壮性，代码能够被多个线程共享，代码和数据是独立的

2. > 适合多个相同的代码的线程区处理同一个资源的情况