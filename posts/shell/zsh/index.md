---
layout: default
menu: menu.html
---

# Zsh (oh-my-zsh) 环境配置

## 介绍

### 什么是Shell？

很多人认为Windows中的CMD / Powershell，macOS中的Terminal和各种Linux桌面环境中各不相同的命令行界面都是Shell。事实上，它们一般被称为Terminal（终端）或Console（控制台），而Shell是其中的一个核心组件。

Shell通常指的是命令行界面的解析器，用于用户和操作系统的直接交互。比如在大部分基于Unix的操作系统（如Linux / macOS）中，默认使用的shell是bash。而Windows不基于Unix，使用微软自己定义的CMD / Powershell作为Shell（Windows中没有特别区分Shell和Terminal）。

这篇教程中，我们主要关注怎么将基于Unix的操作系统中默认的bash替换为zsh，并使用oh-my-zsh框架对zsh进行快速配置。使用Windows的用户可以使用WSL（Windows Subsystem for Linux）进行相似的配置。

注：在下一代macOS Catalina中，zsh将替代bash成为默认shell。

### 什么是zsh？

> [Zsh](https://www.zsh.org/) (Z Shell) 由保罗·弗斯塔德（Paul Falstad）于1990年在普林斯顿大学求学时编写了初版，名称zsh源于耶鲁大学教授邵中（Zhong Shao，后转为普林斯顿大学教授) — 保罗将教授的用户名"zsh"作为此Shell的名称。

Zsh提供了bash的大多数功能，并新增了许多[新特性](https://zh.wikipedia.org/wiki/Z_shell)：
+ 可帮助用户键入常用命令选项及参数的可编程命令行补全功能，自带对数百条命令的支持
+ 可与任意Shell共享命令历史
+ 可在无需运行外部程序（如find）的情况下通过文件扩展匹配文件
+ 改进变量/数组处理方式
+ 在单缓冲区内编辑多行命令
+ 拼写检查
+ ……

### 什么是oh-my-zsh？

GitHub上的“[Oh My Zsh](https://github.com/robbyrussell/oh-my-zsh)”库收集Z shell的第三方插件及主题，并通过简易的配置方式提供一个美观，易用的shell。如下图所示的agnoster主题提供了大部分日常使用所需要显示的内容。

![oh-my-zsh](https://raw.githubusercontent.com/agnoster/agnoster-zsh-theme/master/screenshot.png)

## 安装

### Windows

建议参考[WSL配置教程]()，并使用Linux的配置方法。其中，Powerline字体需要在Windows上安装，下载[Powerline Fonts](https://github.com/powerline/fonts)中心仪的字体并双击安装即可。

### Linux

1. 确保系统中已经安装了zsh，git，curl和fonts-powerline，在Debian/Ubuntu中可以运行：
```bash
sudo apt install zsh git curl fonts-powerline
```


2. 下载并运行oh-my-zsh安装脚本：
```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```


3. 在安装过程中，会提示输入密码将默认的登录shell改为zsh。如果没有成功，可以在安装后运行
```bash
chsh -s /bin/zsh
```


4. 在`~/.zshrc`中修改配置文件。


### macOS

1. 安装Xcode命令行工具获得git（如果提示已安装可以跳过此步）：
```bash
xcode-select --install
```


2. 安装Powerline字体：
```bash
# clone
git clone https://github.com/powerline/fonts.git --depth=1
# install
cd fonts
./install.sh
# clean-up a bit
cd ..
rm -rf fonts
```


3. 下载并运行oh-my-zsh安装脚本：
```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```


4. 在安装过程中，会提示输入密码将默认的登录shell改为zsh。如果没有成功，可以在安装后运行
```bash
chsh -s /bin/zsh
```


5. 在`~/.zshrc`中修改配置文件。

## 配置

成功安装oh-my-zsh后，会在home目录中自动生成`.zshrc`文件，包含了一些默认配置。
修改这个文件后，需要重启Terminal，或者运行以下命令载入配置文件：
```bash
source ~/.zshrc
```

### 主题

在默认的`.zshrc`文件的前几行可以设置主题：

```bash
# Set name of the theme to load --- if set to "random", it will
# load a random theme each time oh-my-zsh is loaded, in which case,
# to know which specific one was loaded, run: echo $RANDOM_THEME
# See https://github.com/robbyrussell/oh-my-zsh/wiki/Themes
ZSH_THEME="robbyrussell"

# Set list of themes to pick from when loading at random
# Setting this variable when ZSH_THEME=random will cause zsh to load
# a theme from this variable instead of looking in ~/.oh-my-zsh/themes/
# If set to an empty array, this variable will have no effect.
# ZSH_THEME_RANDOM_CANDIDATES=( "robbyrussell" "agnoster" )
```

在[主题展示](https://github.com/robbyrussell/oh-my-zsh/wiki/Themes)中，可以看到大部分常用主题的截图，选择你最喜欢的主题吧！

然后修改`ZSH_THEME`来设置zsh的主题，如果想得到开头图片中的效果，需要设置为`agnoster`主题。同时，也可以使用`ZSH_THEME_RANDOM_CANDIDATES`设置多个主题并随机使用。其他配置都可以在#开头的注释行中找到解释。

### 插件

在`.zshrc`文件，还可以设置插件，默认安装了`git`插件。

```bash
# Which plugins would you like to load?
# Standard plugins can be found in ~/.oh-my-zsh/plugins/*
# Custom plugins may be added to ~/.oh-my-zsh/custom/plugins/
# Example format: plugins=(rails git textmate ruby lighthouse)
# Add wisely, as too many plugins slow down shell startup.
plugins=(
  git
)
```

运行`ls ~/.oh-my-zsh/plugins`可以得到官方插件的列表，也可以下载第三方插件并放入`~/.oh-my-zsh/custom/plugins/`目录。


### Powerline字体

安装Powerline特殊字体是为了解决以下一些utf-8字符的乱码问题（可以自己输入检验当前字体是否支持Powerline）：

![characters](https://raw.githubusercontent.com/agnoster/agnoster-zsh-theme/master/characters.png)

字体安装成功后，在Terminal或Console中将字体替换为包含“Powerline”的字体就能正确显示以上特殊字符了。

## 更新

当oh-my-zsh检测到更新时，会自动提示更新，输入`Y`即可直接更新的最新版本。也可以手动运行`upgrade_oh_my_zsh`进行更新。

## 卸载

在shell中运行`uninstall_oh_my_zsh`可以卸载全部配置文件并恢复原来的bash或zsh配置文件。
