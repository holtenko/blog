---
title: Tomcat常见错误
toc: true
date: 2018-01-30 11:35:26
categories: [Java]
tags: [Java,Tomcat,Error,Wiki]
---

## HTTP Status 500 - java.lang.IllegalStateException: No output folder 

### 原因

此错误一般是由于解压缩版的Tomcat没有合理分配权限导致的。

### 解决方案

可通过修改Tomcat目录权限，或修改其拥有者来解决。

1. 修改Tomcat目录权限：`sudo chmod -R 777 $TOMCAT_HOME`。
2. 修改拥有者：`sudo chown -R yourUserName $TOMCAT_HOME`。
