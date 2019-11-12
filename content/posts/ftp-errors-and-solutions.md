---
title: FTP常见错误及解决方案
date: 2017-09-18 15:27:00
categories: [Linux]
tags: [Linux,FTP,Wiki,Error]
---

## 227 Entering Passive Mode
```shell
响应: 227 Entering Passive Mode (192,168,1,16,221,111).
命令: LIST
错误: 连接超时
错误: 读取目录列表失败
```

*解决方法：*
1. 打开`/etc/vsftpd/vsftpd.conf`在最后面加入如下：
```shell
pasv_min_port=1
pasv_max_port=30999
```
2. 在iptable防火墙规则中加入如下规则：
打开`/etc/sysconfig/iptables`加入如下：
```shell
-A INPUT -m state –state NEW -m tcp -p tcp –dport 1:30999 -j ACCEPT
```
3. 重启vsftp和iptables服务了。
* 重启vsftp服务`service vsftpd restart`
* 重启iptables服务`service iptables restart`
