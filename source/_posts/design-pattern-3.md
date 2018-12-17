---
title: 没事学点设计模式-抽象工厂模式
date: 2018-02-12 13:56:14
categories: Basic
tags:
- 设计模式
---
### 系列回顾
1. [没事学点设计模式-概览](http://blog.holten.site/2017/09/11/design-pattern-1/)
2. [没事学点设计模式-工厂模式](http://blog.holten.site/2017/09/29/design-pattern-2/)

### 简介
抽象工厂模式（Abstract Factory Pattern）是围绕一个超级工厂创建其他工厂。该超级工厂又称为其他工厂的工厂。这种类型的设计模式属于创建型模式，它提供了一种创建对象的最佳方式。

在抽象工厂模式中，接口是负责创建一个相关对象的工厂，不需要显式指定它们的类。每个生成的工厂都能按照工厂模式提供对象。
<!-- more -->
**举例说明**
iPhone 8和iPhone X的屏幕和外壳都是不一样的，通过抽象工厂模式就可以实现，在为iPhone生产配件的时候不用指定相关的型号，可以自动根据手机的型号生产相应的配件。

**优点**
当一个系列中的多个对象被设计成一起工作时，它能保证调用时始终只使用同一个系列中的对象，而不需要去指定具体的型号。

**缺点**
系列扩展非常困难，要增加一个系列的某一产品时，既要在抽象的 Factory 里加代码，又要在具体的实现里面加代码。比如后面发现iPhone X配AirPods，iPhone 8配EarPods，那么不仅要Factory接口中添加方法，还要在其实现类中去修改。

**使用场景**
1. 软件的更换界面主题功能；
2. 生成不同操作系统的软件；

### 实例
1.首先需要创建一个Screen、Shell接口和其实现类：
```java
public interface Screen {
    void build();
}

public class Screen8 implements Screen {
    @Override
    public void build() {
        System.out.println("iphone 8 screen get!");
    }
}

public class ScreenX implements Screen {
    @Override
    public void build() {
        System.out.println("iphone X screen get!");
    }
}
```
```java
public interface Shell {
    void build();
}

public class Shell8 implements Shell {
    @Override
    public void build() {
        System.out.println("iphone 8 shell get!");
    }
}

public class ShellX implements Shell {
    @Override
    public void build() {
        System.out.println("iphone X shell get!");
    }
}
```

2.然后定义抽象工厂接口IphoneFactory
```java
public interface IphoneFactory {
    Screen getScreen();

    Shell getShell();
}
```

3.实现相应的工厂
```java
public class Iphone8Factory implements IphoneFactory {
    @Override
    public Screen getScreen() {
        return new Screen8();
    }

    @Override
    public Shell getShell() {
        return new Shell8();
    }
}

public class IphoneXFactory implements IphoneFactory {
    @Override
    public Screen getScreen() {
        return new ScreenX();
    }

    @Override
    public Shell getShell() {
        return new ShellX();
    }
}
```

4.可以生产了
```java
public class AbstractFactoryDemo {

    public static void main(String[] args) {
        IphoneFactory factory = new IphoneXFactory();
        Screen screen = factory.getScreen();
        Shell shell = factory.getShell();
        screen.build();
        shell.build();
    }
}
```

### 本文源码已托管至GitHub，欢迎Star
[抽象工厂模式源码：https://github.com/holtenko/DesignPatterns/tree/master/src/AbstractFactory](https://github.com/holtenko/DesignPatterns/tree/master/src/AbstractFactory)