---
title: BuildMyBlogSystem
tags: [随笔, first]
date: 2018-11-02 22:12:01
---

# 搭建个人Blog教程

其实搭建个人的Blog，一方面是督促自己写Blog的习惯，也是希望自动动手丰衣足食。下面说一下完整搭建一套Blog需要的主要工具。
### Blog框架 - [Hexo](https://hexo.io/)
既然是要自己搭建Blog，那自然需要一个成熟的框架，找来找去，最后还是选择了Hexo
![Hexo](http://phiky9lnw.bkt.clouddn.com/hexo-io.png)
个人使用下来有以下优点：
- 支持Markdown语法；
- 部署方便；
- 插件、主题众多；

尤其是支持Markdown是选择其的最主要原因，因为在你编辑的时候，再去选择什么格式、颜色、字体大小之类，可谓相当之烦。

Hexo的部署，因为官方文档已经很详细了。所以这里简单整理一下。
#### 安装
如果安装了Node.js，可直接用Node的包管理工具[npm](https://www.npmjs.com.cn/)则直接安装hexo-cli命令行工具即可，跳过以下安装步骤
```
$ npm install -g hexo-cli
```
如果没有则按照下面步骤，安装后再回来
安装Node.js，如果安装了nvm包管理工具，可以直接安装，跳过以下安装步骤

```
$ nvm install stable
# 如果想安装其他Node版本也可以：nvm ls-remote 先查看有哪些版本， nvm install [version] 安装需要的版本
```
如果没有安装，可以按照以下步骤安装

* 安装[Homebrew](https://brew.sh/index_zh-cn)，为了安装nvm
```
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
* 安装[nvm](http://nvm.sh)(nvm就是Node的版本管理工具)，为了安装Node
```
$ brew install nvm
# 配置nvm全局变量
$ echo "source $(brew --prefix nvm)/nvm.sh" >> .bash_profile
$ . ~/.bash_profile
# 当然也可以用 $ curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash 安装nvm
```

其中涉及的有NodeJs、nvm和npm，他们三者的关系，如下图
 - nvm:nodeJs版本管理工具,管理nodejs版本和npm版本 
 - nodeJs: reactNative开发过程中所需要的代码库。
 - npm:是随同nodeJs一起安装的包管理工具，npm管理对应nodeJs的第三方插件

![Node、nvm和npm](http://phiky9lnw.bkt.clouddn.com/node.png)
**没有安装Git的话，可以吧Git也装了，后面需要用的**
>⚠️你在编译时可能会碰到问题，请先至App Store安装Xcode，一旦Xcode安装完成后，开启它并前往Preferences -> Download -> Command Line Tools -> Install安装命令列工具
>
>

### - 服务器 - Amazon
### - 域名 - 阿里云
### - DNS - 阿里云
### - 图片存储 - 七牛
### - Git库