---
title: 没事学点设计模式-概览
date: 2017-09-11 15:27:00
categories: [设计模式]
tags: [设计模式]
---
### 什么是设计模式

设计模式是一套被反复使用的、多数人知晓的、经过分类编目的、代码设计经验的总结。设计模式使代码编制真正工程化，可以说设计模式是软件工程的基石。合理的使用设计模式可以使我们的代码具有更强的复用性和灵活的扩展性，这里面蕴含了很多前辈的经验，可以帮助我们少走很多弯路，完美地解决很多问题。

### 有哪些设计模式

根据GOF所著的《设计模式-可复用的面向对象软件元素》中提到，共有23种设计模式。这些模式可以分为三大类：创建型模式（Creational Patterns）、结构型模式（Structural Patterns）、行为型模式（Behavioral Patterns）。

|模式 | 描述 |细分类型|
| :-------: |:-------|:-----|
|创建型模式|这些设计模式提供了一种在创建对象的同时隐藏创建逻辑的方式，而不是使用 new 运算符直接实例化对象。这使得程序在判断针对某个给定实例需要创建哪些对象时更加灵活.|[工厂模式（Factory Pattern）](/2017/09/29/design-pattern-2)<br>[抽象工厂模式（Abstract Factory Pattern）](/2018/02/12/design-pattern-3)<br>[单例模式（Singleton Pattern](/2018/03/22/design-pattern-4)<br>建造者模式（Builder Pattern）<br>原型模式（Prototype Pattern）|
|结构型模式|这些设计模式关注类和对象的组合。继承的概念被用来组合接口和定义组合对象获得新功能的方式。|适配器模式（Adapter Pattern）<br>桥接模式（Bridge Pattern）<br>过滤器模式（Filter、Criteria Pattern）<br>组合模式（Composite Pattern）<br>装饰器模式（Decorator Pattern）<br>外观模式（Facade Pattern）<br>享元模式（Flyweight Pattern）<br>代理模式（Proxy Pattern）|
|行为型模式|这些设计模式特别关注对象之间的通信。|责任链模式（Chain of Responsibility Pattern）<br>命令模式（Command Pattern）<br>解释器模式（Interpreter Pattern）<br>迭代器模式（Iterator Pattern）<br>中介者模式（Mediator Pattern）<br>备忘录模式（Memento Pattern）<br>观察者模式（Observer Pattern）<br>状态模式（State Pattern）<br>空对象模式（Null Object Pattern）<br>策略模式（Strategy Pattern）<br>模板模式（Template Pattern）<br>访问者模式（Visitor Pattern）|

### 设计模式的原则

1. 开闭原则（Open Close Principle）
对扩展开放，对修改关闭。在程序需要进行扩展的时候，不去修改原代码，实现热插拔效果。目的是为了使程序的扩展性好，易于维护和升级。为此需要使用接口和抽象类。
2. 里氏代换原则（Liskov Substitution Principle）
里氏代换原则是面向对象设计的基本原则之一。任何基类可以出现的地方，子类一定可以出现。这个原则是继承复用的基石，只有当派生类可以替换掉基类，且软件单位的功能不受到影响时，基类才能真正被复用，而派生类也能够在基类的基础上增加新的行为。里氏代换原则是对开闭原则的补充。实现开闭原则的关键步骤就是抽象化，而基类与子类的继承关系就是抽象化的具体实现，所以里氏代换原则是对实现抽象化的具体步骤的规范。
3. 依赖反转原则（Dependence Inversion Principle）
这是开闭原则的基础。针对接口编程，依赖于抽象而不依赖于具体。
4. 接口隔离原则（Interface Segregation Principle）
使用多个隔离的接口，比使用单个接口要好。此外还可以降低类之间的耦合度。
5. 迪米特法则，又称最少知道原则（Demeter Principle）
一个实体应当尽量少地与其他实体之间发生相互作用，使得系统功能模块相对独立。
6. 合成复用原则（Composite Reuse Principle）
尽量使用合成/聚合的方式，而不是使用继承。

**后面的文章会详细介绍其中部分设计模式**