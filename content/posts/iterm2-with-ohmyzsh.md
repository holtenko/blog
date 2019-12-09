---
title: iTerm2和oh-my-zsh的个性化定制
date: 2016-03-17 19:55:58
categories: [Shell]
tags: [Shell,Install]
---
终于在某东做活动新入手了一台air，看身边小伙伴的mac的终端感觉好炫酷，于是乎准备自己也捯饬捯饬，google了一下，发现了osx平台上的终端神器iTerm2和用来代替bash的oh-my-zsh，试了一下发现是真的好使，谁用谁知道。

<!-- more -->

![iterm2](https://tva1.sinaimg.cn/large/006tNbRwgy1g9qgln5wolj31400p0n4b.jpg)

#### 安装iTerm2
1. 首先你得先下载一个[iTerm2](http://www.iterm2.com/)。
2. 怎么在osx上安装不用说了，直接copy。
3. 安装完成。

#### 安装oh-my-zsh
直接在iTerm2里面输入：
`sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"`即可。
> 注意啦，执行之前记得先装好git。

### 到这里其实已经安装完成了，下面是个性化定制的内容

#### 安装Powerline
直接在iTerm2里面输入：

```{shell}
sudo easy_install pip
pip install powerline-status
```

安装完成。

#### 安装[字体库](https://github.com/powerline/fonts)
下载下来之后在终端里执行字体库目录下面的install.sh安装powerline字体。

#### 设置iTerm 2的字体
安装完字体库之后，把iTerm 2的偏好设置里的Profile选项卡下面的Text选项卡中里的Regular Font和Non-ASCII Font的字体都设置成 Powerline的字体，喜欢哪个自己选就好了，后面带for powerline的就行。

#### 安装[配色方案](https://github.com/altercation/solarized)
1. 下载下来之后解压，然后到目录下双击Solarized Dark.itermcolors和Solarized Light.itermcolors两个文件就可以把配置文件导入到iTerm 2里。
2. 通过load presets选择刚刚安装的配色主题即可。
3.
#### 安装[agnoster](https://github.com/fcamblor/oh-my-zsh-agnoster-fcamblor)主题
1. 下载下来之后解压，然后到目录里面运行install文件，就可以主题安装到`~/.oh-my-zsh/themes`目录下
2）`cd`切换到用户根目录，打开.zshrc文件，然后将ZSH_THEME后面的字段改为agnoster即可。像这样ZSH_THEME="agnoster"。

### 终于搞完了！
