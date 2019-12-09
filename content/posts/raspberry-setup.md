---
title: 树莓派系统安装配置
date: 2017-09-13 15:27:00
categories: [Linux]
tags: [Linux,Raspberry,Wiki]
---

## 系统安装

1. 格式化内存卡。一定要为**FAT32**，Windows下32G以上内存卡可用[guiformat-x64.exe](http://pan.baidu.com/s/1kUEPxaf)格式化。
2. 将[NOOBS_v2_0_0.zip](http://pan.baidu.com/s/1qYwE7yW)解压，然后将解压后的文件夹内的所有文件复制到内存卡。
3. 将内存卡插入树莓派，使用5V，至少2A以上电源供电，连接显示器，启动树莓派。
4. 在此选择默认的Raspbian，点击Install进行安装。

## 系统更新

1. 连接网络，确认网络可用。
2. 命令行执行`sudo apt-get update`
3. 命令行执行`sudo apt-get upgrade`

## 配置常用环境

### 语言环境

`Preference-Raspberry Pi Configuration-Localisation-Set Locale...`

选择`zh(Chinese)`。
==== 时区环境 ====
`Preference-Raspberry Pi Configuration-Localisation-Set Timezone...`

选择`Asia，Shanghai`。

### 其它环境

开启`Preference-Raspberry Pi Configuration-Interface-SSH`。

其它如Keyboard，WiFi Country自己设置一下为China。

### Java环境配置

1. Java路径：`/usr/lib/jvm/jdk-x-xxx`，具体路径的最后一层可能会有更新。
2. 配置环境变量`vim /etc/profile`,在文件最后添加如下内容

```{shell}
export JAVA_HOME=/usr/lib/jvm/jdk-x-xxx
export JRE_HOME=$JAVA_HOME/jre
export PATH=$PATH:$JAVA_HOME/bin
export CLASSPATH=.:$JAVA_HOME/lib:$JRE_HOME/lib
```

保存文件，然后执行以下`source /etc/profile`,使配置文件生效即可。
