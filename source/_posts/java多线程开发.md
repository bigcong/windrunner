title: 多线程
author: bigcong
tags:
  - 多线程
categories: []
date: 2017-04-24 06:16:00
---
### 多线程
#### interrupted
测试当前线程是否已经中断，线程的中断状态由该方法清除。换句话说，如果连续调用该方法，则第二次调用返回false（在一次调用的时候，已清除了其中的状态之后，且第二次调用检查完中断状态，当前线程再次中断中断除外）


### 留意i-- 和System.out.println()的异常

```
	public class MyThread extends Thread {
    private int i = 5;

    @Override
    public void run() {
        System.out.println("i=" + i--);


    }

    public static void main(String[] args) throws InterruptedException {
        MyThread a = new MyThread();
        Thread b1 = new Thread(a);
        Thread b2 = new Thread(a);
        Thread b3 = new Thread(a);
        Thread b4 = new Thread(a);
        Thread b5 = new Thread(a);
        b5.start();
        b2.start();
        b4.start();
        b3.start();
        b1.start();
    }
}


```
```
public class MyThread extends Thread {
    private int i = 5;

    @Override
    public void run() {
        i--;
        System.out.println("i=" +i);


    }

    public static void main(String[] args) throws InterruptedException {
        MyThread a = new MyThread();
        Thread b1 = new Thread(a);
        Thread b2 = new Thread(a);
        Thread b3 = new Thread(a);
        Thread b4 = new Thread(a);
        Thread b5 = new Thread(a);
        b5.start();
        b2.start();
        b4.start();
        b3.start();
        b1.start();


    }
}

```
以上代码执行的结果不一样的，是因为println方法，加了线程锁

```
    public void println(String x) {
        synchronized (this) {
            print(x);
            newLine();
        }
    }

```
