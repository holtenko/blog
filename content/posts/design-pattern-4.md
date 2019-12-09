---
title: 没事学点设计模式-单例模式
date: 2018-03-22 14:37:45
categories: [设计模式]
tags: [设计模式]
---
### 系列回顾
1. [没事学点设计模式-概览]({{< relref "design-pattern-1.md" >}})
2. [没事学点设计模式-工厂模式]({{< relref "design-pattern-2.md" >}})
3. [没事学点设计模式-抽象工厂模式]({{< relref "design-pattern-3.md" >}})

### 简介
单例模式（Singleton Pattern）可以说是Java中最简单的设计模式。这种类型的设计模式属于创建型模式，它提供了一种创建一个全局唯一对象的最佳方式，可以避免一个全局使用的对象，尤其是大对象，的频繁创建与销毁。

这种模式涉及到一个单一的类，该类负责创建自己的对象实例，同时确保只有一个对象实例被创建。这个类提供了访问其唯一的对象的方式，可以直接访问，不需要实例化该类的对象。这就意味着单例类只能有一个实例，而且必须自己给自己创建唯一的实例，同时必须给其他所有对象提供这一实例。
<!-- more -->
**优点**
 1. 在单例模式中，对单例类的所有实例化得到的都是相同的一个实例，可以确保所有的对象都访问同一个实例。
 2. 类自己来控制实例化进程，类就在改变实例化进程上有相应的伸缩性。
 3. 提供了对唯一实例的受控访问。
 4. 由于在系统内存中只存在一个对象，因此可以节约系统资源，当需要频繁创建和销毁的对象，特别是大对象时可以提高系统的性能。
 5. 避免对共享资源的多重占用。

**缺点**
1. 无法继承，扩展比较困难。
2. 不适用于变化的对象。

### 实例
单例模式的实现有非常多，但是有些是线程安全的，有些是线程不安全的，这里仅介绍几种线程安全的实现方法。

#### 懒汉式
这种方式可以实现懒加载，线程安全，但是会存在效率问题，因为绝大多数情况下是不需要同步加锁的。

**代码如下：**

```{java}
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
```

#### 饿汉式

这种方式基于classloader机制避免了线程安全问题，但是实例在类加载时就实例化了，可能会产生垃圾对象。

**代码如下：**

```{java}
public class Singleton {  
    private static Singleton instance = new Singleton();  
    private Singleton (){}  
    public static Singleton getInstance() {  
    return instance;  
    }  
}
```

#### 双重校验式

这种方式采用双重校验锁的机制，可以保证线程安全且可以保证较好的性能。

**代码如下：**

```{java}
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
```

#### 静态内部类式

这种方式和饿汉式采用相同的机制来保证线程安全，但是通过静态内部类的形式实现了懒加载，避免了垃圾对象的产生。

**代码如下：**

```{java}
public class Singleton {  
    private static class SingletonHolder {  
    private static final Singleton INSTANCE = new Singleton();  
    }  
    private Singleton (){}  
    public static final Singleton getInstance() {  
    return SingletonHolder.INSTANCE;  
    }  
}
```

#### 枚举式

这种方式在实际使用中很少被采用，但是这确实是目前实现单例最好的方式，简洁，自动支持序列化机制，绝对防止多次实例化，也无法通过反射调用构造函数的方式来创建实例。

**代码如下：**

```{java}
public enum Singleton {  
    INSTANCE;  
    public void yourMethod() {  
    }  
}  
```

### 本文源码已托管至GitHub，欢迎Star
[抽象工厂模式源码：https://github.com/holtenko/DesignPatterns/tree/master/src/Singleton](https://github.com/holtenko/DesignPatterns/tree/master/src/Singleton)