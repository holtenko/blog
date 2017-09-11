title: CentOS下通过源码安装最新版Git
date: 2015-12-05 14:53:30
categories: Git
tags:
- Git
- 安装
---
#### 下载源码
到Git的Github主页上下载最新的源码到本地，解压并进入目录。

#### 编译安装
```bash
cd 你的git源码目录
autoconf
./configure
make
```
<!-- more -->
#### 第一个报错
**报错内容：**
```bash
usr/bin/perl Makefile.PL PREFIX='/usr/local/git' INSTALL_BASE='' --localedir='/usr/local/git/share/locale'
Can't locate ExtUtils/MakeMaker.pm in @INC (@INC contains: /usr/local/lib64/perl5 /usr/local/share/perl5 /usr/lib64/perl5/vendor_perl /usr/share/perl5/vendor_perl /usr/lib64/perl5 /usr/share/perl5 .) at Makefile.PL line 3.
BEGIN failed--compilation aborted at Makefile.PL line 3.
make[1]: *** [perl.mak] Error 2
make: *** [perl/perl.mak] Error 2
```
**解决方法：**
```bash
yum install perl-ExtUtils-MakeMaker package
```

#### 第二个报错
**报错内容：**
```bash
tclsh failed; using unoptimized loading
MSGFMT    po/bg.msg make[1]: *** [po/bg.msg] 错误 127
```
**解决方法：**
yum install tcl  build-essential tk gettext

#### 继续编译安装
```bash
make
make install
```
终于世界清净了
#### 建立软链接
```bash
ln -s /usr/local/bin/git /usr/bin
git --version
```
出现了
```bash
git version 2.6.0.GIT
```
至此，**安装完成**。
