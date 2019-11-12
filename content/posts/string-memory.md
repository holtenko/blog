---
title: Java中字符串内存位置浅析
date: 2016-08-16 13:12:56
categories: [Java]
tags: [Java,内存,String]
---
### 前言
之前写过一篇关于[JVM内存区域划分](http://blog.holten.site/2016/04/09/JVM-memory-area/)的文章，但是昨天接到蚂蚁金服的面试，问到JVM相关的内容，解释一下JVM的内存区域划分，这部分答得还不错，但是后来又问了Java里面String存放的位置，之前只记得String是一个不变的量，应该是要存放在常量池里面的，但是后来问到new一个String出来应该是放到哪里的，这个应该是放到堆里面的，后来又问到String的引用是放在什么地方的，当时傻逼的说也是放在堆里面的，现在总结一下：基本类型的变量数据和对象的引用都是放在栈里面的，对象本身放在堆里面，显式的String常量放在常量池，String对象放在堆中。
<!-- more -->
### 常量池的说明
常量池之前是放在方法区里面的，也就是在永久代里面的，从JDK7开始移到了堆里面。这一改变我们可以从oracle的[release version](http://www.oracle.com/technetwork/java/javase/jdk7-relnotes-418459.html)的notes里的** Important RFEs Addressed in JDK 7 **看到。
```
Area: HotSpot
Synopsis: In JDK 7, interned strings are no longer allocated in the permanent 
generation of the Java heap, but are instead allocated in the main part of the 
Java heap (known as the young and old generations), along with the other 
objects created by the application. This change will result in more data 
residing in the main Java heap, and less data in the permanent generation, and 
thus may require heap sizes to be adjusted. Most applications will see only 
relatively small differences in heap usage due to this change, but larger 
applications that load many classes or make heavy use of the String.intern() 
method will see more significant differences.
RFE: 6962931
```

### String内存位置说明
1.显式的String常量
```Java
String a = "holten";
String b = "holten";
```
- 第一句代码执行后就在常量池中创建了一个值为holten的String对象；
- 第二句执行时，因为常量池中存在holten所以就不再创建新的String对象了。
- 此时该字符串的引用在虚拟机栈里面。

2.String对象
```Java
String a = new String("holtenObj");
String b = new String("holtenObj");
```
- Class被加载时就在常量池中创建了一个值为holtenObj的String对象，第一句执行时会在堆里创建new String("holtenObj")对象；
- 第二句执行时，因为常量池中存在holtenObj所以就不再创建新的String对象了，直接在堆里创建new String("holtenObj")对象。

### 验证一下
```Java
/**
 * Created by holten.gao on 2016/8/16.
 */
public class Main {
    public static void main(String[] args){
        String str1 = "高小天";
        String str2 = "高小天";
        System.out.println(str1==str2);//true
        
        String str3 = new String("高大天");
        String str4 = new String("高大天");
        System.out.println(str3==str4);//false
    }
}
```
返回结果：
```Java
true
false
```
