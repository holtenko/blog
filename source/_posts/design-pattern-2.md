---
title: 没事学点设计模式-工厂模式
date: 2017-09-29 09:23:52
tags:
- 设计模式
---
#### 系列回顾
1. [没事学点设计模式-概览](http://blog.holten.site/2017/09/11/design-pattern-1/)

### 简介
工厂模式（Factory Pattern）是一种最常用的设计模式。这种类型的设计模式属于创建型模式，它提供了一种方便快捷创建对象的最佳方式。

在工厂模式中，我们在创建对象时不需要向调用方暴露创建对象的具体逻辑流程，并且是通过使用一个共同的接口来指向新创建的对象。工厂模式定义一个创建对象的接口，让其子类自己决定实例化哪一个工厂类，工厂模式使其创建过程延迟到子类进行，用以解决接口选择的问题。

**举例说明**
 1. 我要买一辆汽车，我可以直接从工厂里面提货，而不用去关心这辆汽车是如何生产出来的，以及这个汽车里面的各种细节是什么样子的。
 2. 我要买一部手机，我也不需要知道手机是怎么制造出来的，我只需要知道我想要iPhoneX还是还是HUAWEI P10，工厂自然会帮我制造出来。

**优点**
1. 创建一个对象，只要知道其名称就可以了，就比如我只需要知道那款手机叫iPhoneX就可以了；
2. 扩展性高，如果想增加一个产品，只要扩展一个工厂类就可以了；
3. 屏蔽具体实现，用户只关心接口即可。

**缺点**
每增加一个实现时，都需要增加一个具体类和对象实现工厂，使得系统中类的个数成倍增加，在一定程度上增加了系统的复杂度，同时也增加了系统具体类的依赖。

**使用场景**
1. 日志记录器：记录可能记录到本地文件、远程服务器、打印到终端等，用户只需要知道要记录到哪里说明即可。
2. 数据库访问：当用户不知道最后系统采用哪一类数据库，以及数据库可能有变化时，现在是Oracle，有可能换到MySQL等，此时只需换方言和驱动就可以。
3. 设计一个连接服务器的框架，可以通过"TCP"或者"UDP"或者其他协议,可以把这些都作为产品类，共同实现一个接口即可。

### 实例
我们以生产iPhone的生产工厂为例。

1.首先需要创建一个iphone接口和其实现类：接口iphone，实现类iphone7\iphone8\iphonex；
```java
public interface iphone {
    void build();
}
```
```java
public class iphone7 implements iphone {
    @Override
    public void build() {
       System.out.println("iphone7 get!");
    }
}
```
```java
public class iphone8 implements iphone {
    @Override
    public void build() {
        System.out.println("iphone8 get!");
    }
}
```
```java
public class iphonex implements iphone {
    @Override
    public void build() {
        System.out.println("iphonex get!");
    }
}
```
2.然后定义工厂类iphoneFactory
```java
public class iphoneFactory {
   public Shape getIphone(String iphoneType){
        if(iphoneType == null){
         return null;
        }        
        if(iphoneType.equalsIgnoreCase("iphone7")){
         return new iphone7();
        } else if(iphoneType.equalsIgnoreCase("iphone8")){
         return new iphone8();
        } else if(iphoneType.equalsIgnoreCase("iphonex")){
         return new iphonex();
        }
        return null;
   }
}
```
3.然后就可以随意生产了，比如先来一个iphonex哈哈哈
```java
iphoneFactory iphonefactory = new iphoneFactory();
iphone iphone1 = iphonefactory.getShape("iphonex");
iphone1.draw();
```