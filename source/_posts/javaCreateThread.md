---
title: Java中创建线程的两种方式
date: 2016-10-17 16:10:15
categories: Java
tags: 
- Java
- 线程
- Thread
---

#### 前言
多线程是我们开发过程中经常遇到的，也是必不可少需要掌握的。当我们知道需要进行多线程开发时首先需要知道的自然是如何实现多线程，也就是我们应该如何创建线程。

在Java中创建线程和创建普通的类的对象操作是一样的，我们可以通过两种方式来创建线程：
1. 继承Thread类，并重写run()方法。
2. 实现Runnable接口，并实现run()方法。

#### 方法一：继承Thread类
代码非常简单
1. 首先重载一个构造函数，以便我们可以给线程命名。
2. 重写run()方法。
3. 这里我们先让线程输出线程名+start。
4. 然后每5ms输出线程名+一个递增数。

```java
/**
 * Created by holten.gao on 2016/10/17.
 */
public class threadThread extends Thread {
    public threadThread(String name) {
        super(name);
    }

    @Override
    public void run() {
        System.out.println(this.getName()+" start!");
        for(int i=0;i<10;i++){
            System.out.println(this.getName()+" "+i);
            try {
                Thread.sleep(5);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
```

#### 方法二：实现Runnable接口
代码也非常简单
1. 实现run()方法。
2. 这里我们先让线程输出线程名+start。
3. 然后每5ms输出线程名+一个递增数。

```java
/**
 * Created by holten.gao on 2016/10/17.
 */
public class runnableThread implements Runnable {
    @Override
    public void run() {
        System.out.println(Thread.currentThread().getName()+" start!");
        for(int i=0;i<10;i++){
            System.out.println(Thread.currentThread().getName()+" "+i);
            try {
                Thread.sleep(5);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
```

#### 测试结果
测试代码
```java
/**
 * Created by holten.gao on 2016/10/17.
 */
public class Main {
    public static void main(String[] args) {
        Thread threadThread=new threadThread("threadThread");
        threadThread.start();
        Thread runnableThread=new Thread(new runnableThread(),"runnableThread");
        runnableThread.start();
    }
}
```


测试结果
```bash
threadThread start!
threadThread 0
runnableThread start!
runnableThread 0
threadThread 1
runnableThread 1
threadThread 2
runnableThread 2
threadThread 3
runnableThread 3
threadThread 4
runnableThread 4
threadThread 5
runnableThread 5
threadThread 6
runnableThread 6
threadThread 7
runnableThread 7
threadThread 8
runnableThread 8
threadThread 9
runnableThread 9
```

#### 两种方法比较
1. 因为Java只支持单继承，所以使用方法一就不能再继承其他类了；而方法二实现接口则不会影响继承其他类。
2. 方法一由于是继承Thread，所以直接new出来就可以start；而方法二需要将对象作为参数传入Thread对象才能得到Thread对象。
3. 方法一中可以直接通过this.getName获得线程名；而方法二需要Thread.currentThread().getName()获得