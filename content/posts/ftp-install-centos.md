---
title: CentOS下FTP服务器安装与配置
date: 2017-09-17 15:27:00
categories: [Linux]
tags: [Linux,FTP,Wiki]
---

## 安装vsftpd

```{shell}
yum install vsftpd
```

## 启动/重启/关闭vsftpd服务器

CentOS7 以下：
* 启动: `service vsftpd start`
* 停止: `service vsftpd stop`
* 重启: `service vsftpd restart`
* 执行完成后可以使用`service vsftpd status`查看运行状态
* CentOS7：
* 启动: `/bin/systemctl start vsftpd.service`
* 停止: `/bin/systemctl stop vsftpd.service`
* 重启: `/bin/systemctl restart vsftpd.service`
* 执行完成后可以使用`/bin/systemctl status vsftpd.service`查看状态

## 与vsftpd服务器有关的文件和文件夹

* vsftpd服务器的配置文件的是: `/etc/vsftpd/vsftpd.conf`

## 定制进入FTP服务器的欢迎信息

在vsftpd.conf文件中设置:`dirmessage_enable=yes`,然后进入用户目录建立一个`.message`文件,输入欢迎信息即可。

## 设置开机启动

找到/etc/rc.local文件，在最后一行添加：`service vsftpd start` ,保存，退出

## 配置vsftpd.conf

```{shell}
anonymous_enable=NO                                  #禁止匿名
local_enable=YES                                     #允许本地登录
write_enable=YES                                     #允许写，如需上传，则必须
local_umask=027                                      #将上传文件的权限设置为：777-local_umask
anon_upload_enable=YES                               # 允许虚拟用户和匿名用户上传
anon_other_write_enable=YES                          #允许虚拟用户和匿名用户修改文件名和删除文件
dirmessage_enable=YES          
xferlog_enable=YES                                   #打开日志记录
connect_from_port_20=YES
xferlog_file=/var/log/vsftpd.log                     #日志存放位置
xferlog_std_format=YES                               #标准日志格式
idle_session_timeout=600                             #空闲连接超时
data_connection_timeout=120
ftpd_banner=Welcome to Holten FTP service            #欢迎信息
guest_enable=yes                                     #允许虚拟用户
guest_username=vsftpdguest                           #虚拟用户使用的系统账号
virtual_use_local_privs=YES                          #虚拟用户拥有本地系统权限
chroot_local_user=NO              
chroot_list_enable=YES
#以上两行将虚拟用户限制在其目录下，不能访问其他目录，或者直接用                            
chroot_local_user=YES                               
listen=yes                                           #监听/被动模式
listen_port=21                                       #监听端口
chroot_list_file=/etc/vsftpd/vsftpd.chroot_list      #虚拟用户名单保存在文件 /etc/vsftpd/vsftpd.chroot_list 中
user_config_dir=/etc/vsftpd/vsftpd_user_conf         #每个虚拟用户名的更加详细的配置保存在 /etc/vsftpd/vsftpd_user_conf 中
```
