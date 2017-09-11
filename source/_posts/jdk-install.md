title: Linux环境下RPM方式JDK安装及配置
date: 2015-11-25 13:48:22
categories: Java
tags: 
- Java
- 安装
- jdk
---
#### jdk下载
这个到java的[官方网站](http://www.oracle.com/technetwork/java/javase/downloads/index-jsp-138363.html)下载自己需要的版本就好了，这里下载了jdk1.7版本的，选择下载了rpm包jdk-7u79-linux-x64.rpm。
<br/>
#### rpm安装
```{bash}
rpm -ivh jdk安装包的目录/jdk-7u79-linux-x64.rpm
```
<!-- more -->
***解释一下：***
-i,--install  表示安装软件包 install package(s)
-v,--verbose  表示安装过程中输出软件包更多的信息 provide more detailed output
-h,--hash     表示显示安装进度 print hash marks as package installs (good with -v)
<br/>
#### 配置环境变量
```{bash}
vim /etc/profile
```
在最后添加
```{bash}
export JAVA_HOME=/usr/java/jdk1.7.0_79
export JRE_HOME=$JAVA_HOME/jre
export PATH=$PATH:$JAVA_HOME/bin
export CLASSPATH=.:$JAVA_HOME/lib:$JRE_HOME/lib
```
保存文件，然后执行以下命令使配置文件生效即可。
```{bash}
source /etc/profile
```
最后测试一下
```{bash}
# java -version
java version "1.7.0_79"
Java(TM) SE Runtime Environment (build 1.7.0_79-b15)
Java HotSpot(TM) 64-Bit Server VM (build 24.79-b02, mixed mode)
```
**至此，安装完成！**


