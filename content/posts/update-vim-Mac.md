---
title: Mac下更新Vim到最新版本
date: 2017-09-16 15:27:00
categories: [Tools]
tags: [Tools,Mac,Wiki]
---

目前，Mac内置的Vim是7.3版本的，而且还缺少很多功能，下面介绍如何通过源码安装更新最新版本的Vim，同时保留系统内置的Vim。
```shell
# 下载Vim源代码
git clone https://github.com/vim/vim.git
# 进入源码的src目录
cd vim/src
#配置、安装
./configure --enable-pythoninterp 

make

make install

# 卸载的话 make uninstall 
```
  
此时，Vim被安装在了`/usr/local/bin`下，重启终端后，可以通过`which vim`查看。
  
此时，一般来说在终端里执行vim命令的话就应该是新版本的vim了，需要说明的是，这是因为系统内置的vim在`/usr/bin`目录下，而$PATH里`/usr/local/bin`在`/usr/bin`之前，所以系统会先找到刚安装的vim，所以如果你发现没有使用新版本的vim，请`echo $PATH`查看确认。
