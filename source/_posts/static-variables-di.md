---
title: 静态变量的自动注入值
date: 2017-09-12 18:27:00
categories: [Java]
tags: [Java,Spring,Wiki]
---

做项目的时候有可能会经常发生这样的事情，就是要在静态方法里面调用其他类的方法，如果直接new一个出来的话，有可能会造成该类和该类里面的其他依赖类无法正常的注入，如果直接`@Autowired`在这个静态变量上的话会造成该变量还是null。

## 为什么呢？

因为静态变量不是一个对象，只是类的引用，而类被加载字节码的时候，变量已经初始化了，也就是给该变量分配内存了，导致spring忽略静态变量。

## 如何解决呢？

可以使用`setter`方法来注入，如下：

```java
private static UserService userService；

@Autowired  
public void setUserService(UserService service) {  
    userService = service;  
} 
```

这样就可以正常的进行依赖注入了。
