title: 用Hexo搭建属于自己的Blog
date: 2015-11-17 15:15:21
categories: Hexo
tags: 
- Hexo
- 安装
- 教程
- Setup
---
#### 什么是Hexo
简单的来说，Hexo是一款基于Node.JS的静态博客框架，官方给它的描述是“A fast, simple & powerful blog framework”。据说它是出自台湾大学生Tommy Chen之手，官方网站是[https://hexo.io](https://hexo.io)，不由感叹台湾大学生的创造力，当然大陆的大学生也是很厉害的，只不过表现在不同方面而已。说远了，言归正传，它有什么特殊之处呢，我没有怎么接触过Node.JS，所以在其代码方面没有什么发言权，就说一下使用上的特点，首先生成速度非常快，可以使用Markdown进行编辑，操作非常简单，一键生成部署到GitHub Pages等（当然自己有空间的部署在自己的空间上也是OK的），所有平台可用，还有好多主题啊、插件啊之类的。
<!-- more -->
<br/>
#### 我为什么用Hexo
当初准备搭建个人Blog时是准备在GitHub上搭建，省时省钱省力，GitHub推荐的是使用Jekyll，也是一款静态博客框架，了解了一下它是基于Ruby开发的，之前完全没有接触过Ruby，又不想单单为了写个Blog再去从头学Ruby，倒腾了一上午发现太麻烦了，偶然间发现了Hexo，感觉还挺不错，看了一下文档发现还是非常easy的，于是乎就用了Hexo。
<br/>
#### Hexo的安装步骤
网上有很多Hexo的安装教程，为什么还要写呢，主要是我发现网上教程有些地方写的不是很明白，同时也是做一下记录吧。
##### 1. 安装环境
+ Windows10 64bit
+ Node 4.2.2
+ npm 2.14.7
+ Hexo 3.1.1

##### 2. Node环境安装
+ Windows上直接到[官网](https://nodejs.org)上下载安装包打开安装就OK了。
+ Linux上也是下载对应的编译好的包，然后解压，解压完之后进入bin目录执行就可以了，如果嫌麻烦可以建立一下链接：
```{bash}
ln -s node目录/bin/node /usr/local/bin/node
ln -s node目录/bin/npm /usr/local/bin/npm
```
下面可以用`npm version`命令试一下有没有安装成功，成功的话会有如下显示：
```{bash}
$ npm version
{ 'hexo-site': '0.0.0',
  npm: '2.14.7',
  ares: '1.10.1-DEV',
  http_parser: '2.5.0',
  icu: '56.1',
  modules: '46',
  node: '4.2.2',
  openssl: '1.0.2d',
  uv: '1.7.5',
  v8: '4.5.103.35',
  zlib: '1.2.8' }
```
到此，node环境就安装完成了。

##### 3. 使用npm安装Hexo
```{bash}
npm install hexo-cli -g
```
然后用`hexo version`命令可以确认一下有没有安装成功，成功的话会有如下显示：
```{bash}
$ hexo version
hexo: 3.1.1
os: Windows_NT 10.0.10240 win32 x64
http_parser: 2.5.0
node: 4.2.2
v8: 4.5.103.35
uv: 1.7.5
zlib: 1.2.8
ares: 1.10.1-DEV
icu: 56.1
modules: 46
openssl: 1.0.2d
```
到此，Hexo就**安装完成**啦。

如何使用的部分，下一篇再写吧。
