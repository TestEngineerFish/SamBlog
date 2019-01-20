---
title: 动手搭建一个属于自己的博客系统
tags: [随笔]
date: 2018-11-03 22:12:01
---

# 搭建个人Blog教程

终于搭建完了，也梳理一下整个搭建的过程，自己动动手，还是有收获的，建议大家有空的话，可以自己按照以下步骤自己尝试下。
如果觉得麻烦，还是可以用其他已经搭建好的服务商，比如公众号、简书之列。
书写和理解真的差距很大，平时将自己理解的知识整理书写出来，比一般的记忆强太多，因为书写的过程就是一个梳理加强记忆的过程，甚至在书写的时候会遇到一些理解中模糊的点，也是一个很好的查缺补漏的机会。

### 1、Blog框架 - [Hexo](https://hexo.io/)
既然是要自己搭建Blog，那自然需要一个成熟的框架，找来找去，最后还是选择了Hexo
![Hexo](http://phiky9lnw.bkt.clouddn.com/hexo-io.png)
个人使用下来有以下优点：
- 支持Markdown语法；
- 部署方便；
- 插件、主题众多；

尤其是支持Markdown是选择其的最主要原因，因为在你编辑的时候，再去选择什么格式、颜色、字体大小之类，可谓相当之烦。

Hexo的部署，因为官方文档已经很详细了。所以这里简单整理一下。
#### 1.1 安装
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

#### 1.2 启动服务
如果以上都安装没有问题的话，既可以使用上面安装的hexo-cli命令行工具，直接初始化一个blog目录
```
hexo init BlogProject
```
如果初始化完成应该会得到一下目录
![list](http://phiky9lnw.bkt.clouddn.com/hexoCatelogList.png)
然后直接自动服务，开始的时候会有一个默认的文章hello-world.md
```
hexo s
```
根据提示直接打开url：http://localhost:4000
![default](http://phiky9lnw.bkt.clouddn.com/defaultBlog.png)

着重说下三个目录
 - \_config.yml
hexo的配置文件，包括后面的git和域名配置等都需要在这个文件配置，简单里的理解就是配置一些宏变量
 - source
 文章主目录，包括草稿文章和已发布的文章已经tags和categoies之类，以后编辑文章也是在这个目录，后面细说
 - themes
 blog的存放主题的目录，Hexo有着丰富的[主题库](https://hexo.io/themes/)，当然你时间充裕的话也可以自己定义一个主题
 直接浏览[主题库](https://hexo.io/themes/)，下载自己喜欢的主推，存放到theme目录，然后到_config.yml文件中，修改默认主题
``` yml
theme: hexo-theme-anodyne
```

#### 1.3 编辑Blog
首先修改默认创建的Blog类型为草稿，进入\_config.yml
``` yml
default_layout: draft
```
创建Blog文件
```
hexo new articleTitle
```
创建完成后，既在source目录中会创建一个草稿的_drafts/articleTitle.md，随后找一个你喜欢的编辑器就可以开始编辑文章啦，markdown格式哦，笔者喜欢SublimeText，直接编辑完后Control+S保存即可，刷新网页即会显示最新内容
其他详细的可以再去查[Hexo](https://hexo.io)看官方网站的

#### 1.4 配置Hexo
记得配置以下服务器之后回来修改 **_config.yml** 文件，可以直接将编辑好的文件，部署到服务器上
```
url: http://server-ip # 没有绑定域名时填写服务器的实际 IP 地址。
```
再划到 **_config,yml** 底部，修改deploy
```
deploy:
    type: git
    repo: ubuntu@云服务器的IP地址:/var/repo/hexo_static
    branch: master
```
保存退出
安装Git
```
npm install hexo-deployer-git --save
```
将编辑好的文章部署到服务器
```
hexo generate && hexo deploy
```
对了，如果没有配置ssh的话，会输入密码，这里建议配置ssh
配置很简单，直接获取本机的公钥
```
cat ~/.ssh/id_rsa.pub
```
复制后放到服务器的 **~/.ssh/authorized_keys** 文件中即可
本地没有公钥，可以手动创建一个：**ssh-keygen**

### 2、服务器 - Amazon
Blog可以编辑了，但是我们不能总是在本地开启服务吧，而且外网的用户也无法访问，所以我们需要一个服务器用来存放我们的内容和方便其他外网用户访问。
Amazon有个1年服务器的免费试用优惠，所以……，哈哈，我选择了它，没有其他理由。

#### 2.1 翻墙
毕竟不是国内的服务，总是要有个梯子，这个梯子在我大天朝还是敏感词，所以我在之后的其他文章在详细说如何自己免费搭建一个梯子

#### 2.2 购买一个服务器
没有帐号的需要自己注册一个，然后有一个推荐试用的EC2的服务器，直接选择就好了（我选的ubuntu-18.04-amd64-server），就不细说了哈
进入EC2Dashboard主页 > 进入该实例 > 连接
![ssh](http://phiky9lnw.bkt.clouddn.com/sshAmazon.png)
按照图上，直接链接该服务器
#### 2.3 配置服务器
主要配置完成以下内容
 1、为本地的hexo-blog配置一个部署静态文件的Git仓库
 2、配置Nginx托管Blog文件目录
 3、配置远端仓库自动更新到Blog文件目录的Hook

在配置之前，我们需要在服务中安装我们需要两个主要工具 Nginx和Git
```
sudo apt-get update
sudo apt-get install git nginx -y
sudo apt-get install git
```

1.1 部署静态文件的Git库
在 **/var/repo** 创建一个 **hexo_static** 裸仓库(bare repo)
如果没有该目录，则创建一个并修改权限，使ubuntu账户拥有之后文件的权限

```
sudo mkdir /var/repo/
sudo chown -R $USER:$USER /var/repo/
sudo chmod -R 755 /var/repo/
```

然后执行下面的命令

```
cd /var/repo/
git init --bare hexo_static.git
```
2.1 配置Nginx托管Blog文件目录
创建 **/var/www/hexo** 用户Nginx托管
```
sudo mkdir -p /var/www/hexo
```
一样的，我们需要修改目录权限
```
sudo chown -R $USER:$USER /var/www/hexo
sudo chmod -R 755 /var/www/hexo
```
修改Nginx的设置
```
sudo vim /etc/nginx/sites-available/default
```
将默认的root目录指向  ** /var/www/hexo **
``` conf
...

server {
    listen 80 default_server;
    listen [::]:80 default_server ipv6only=on;

    root /var/www/hexo; # 需要修改的部分
    index index.html index.htm;
...
```
下面配置完域名以后，可以再回到这里，配置Nginx的域名为你购买的域名
重启Nginx服务，使修改生效
```
sudo service nginx restart
```
#### 2.4 配置Git 钩子
在服务器的裸仓库 **hexo-static** 创建一个钩子，在满足特定条件是，将静态的HTML传送到Web服务器 **/var/www/hexo** 目录下

在自动生成的 hooks 目录下创建一个新的钩子文件：
```
vim /var/repo/hexo_static.git/hooks/post-receive
```
在该文件中添加两行代码，指定 Git 的工作树（源代码）和 Git 目录（配置文件等）。
```
#!/bin/bash

git --work-tree=/var/www/hexo --git-dir=/var/repo/hexo_static.git checkout -f
```
保存并退出，修改文件权限为可执行文件
```
chmod +x /var/repo/hexo_static.git/hooks/post-receive
```
服务器暂时配置完成，尝试的，可以回到编辑Blog上面，配置完后可以直接访问IP地址即可看到你编辑的文章了
### 域名 - [阿里云](https://www.aliyun.com)
我们不能总是用IP来访问吧，所以我们需要域名服务，我选择在阿里云注册，其提供免费NDS服务，选了一个自己名字的拼音域名，价格一年二十几元。
登录阿里云管理控制台，选择[域名注册](https://wanwang.aliyun.com/domain/?spm=5176.100251.111252.16.6d4a4f15SMrj32)
![ali_domain](http://phiky9lnw.bkt.clouddn.com/ali_domain.png)
搜索一个我们需要的域名，看是否存在，比如：tingyusha
![tingyusha_domain](http://phiky9lnw.bkt.clouddn.com/tingyusha_domain.png)
列表中包含了各种以 **tingyusha** 开头的域名，自己选择一个，在国内使用，区别已经没有那么细了
加入购物车，结算即可
### DNS - 阿里云
有了域名之后，我们就需要配置域名的NDS服务，就是将我们的域名和我们之前买的服务器地址进行绑定。
进入阿里云域名控制台，在我们刚购买的域名栏右侧，点击【解析】
![domain_view](http://phiky9lnw.bkt.clouddn.com/domin_view.png)
选择【新手引导】或者【添加记录】，绑定我们的服务器的IP到该域名下，可添加多条
![edit_dns](http://phiky9lnw.bkt.clouddn.com/edit_NDS.png)
配置完成后，我们即可将我们购买的域名配置到Hexo配置文件中的url字段上了
```
url: http://www.tingyusha.cn/
```
这时候访问以上IP就等同于访问了我们购买的那个Amazon服务器
### 图片存储 - [七牛](https://portal.qiniu.com/)
编辑Blog经常要用到图片，存储图片是个麻烦事，我们可以在刚才购买的服务器上搭建一个图片存储服务器，但是如果服务器被封，或者其他原因挂了，我们就拿不回来了，所以分开放个人觉得比较保险，所以我选择了七牛云，因为工作上也用的这个平台做图片存储，一直用下来，感觉还是不错的，但是在配置域名的时候遇到个坑！很大的坑！因为我们服务器是国外的，不用备案，但是我们域名是国内的，需要备案，不然七牛不允许你绑定该域名到镜像存储空间，阿里方的域名备案又需要绑定他们自己的服务器，这就麻烦了。所以暂时用的是七牛的测试域名，一个月过期，过期后，可以在文件编辑器中，正则替换图片ur的域名，当然是有解决办法的，比如先绑定一个国内的服务器，过审之后再绑定到国外的域名。
七牛使用还是满简单的，注册帐号后，会有一个免费的账户，个人感觉够用了
![qiniu](http://phiky9lnw.bkt.clouddn.com/qiniu.png)
创建一个存储空间，用于存储图片
![qiniu_data](http://phiky9lnw.bkt.clouddn.com/qiniu_data.png)
刚创建的存储空间默认有一个测试域名，就是我上面说的，能绑定一个有效的正式域名最好，方便后面访问
![qiniu_test_domain](http://phiky9lnw.bkt.clouddn.com/qiniu_test_domain.png)
后面遇到需要的照片，直接传上来就好了，后面可以写个桌面小工具，把图片拖进去，直接上传到七牛，返回对应外链地址都是可以的，七牛支持这方面的调用
### Git库
以上基本上就差不多了，可以直接编辑并发布到个人的服务器，但是我有个个人的需求，可能会在多个地方编辑，这就又需要用到Git库了，将本地的文件直接托管到Git库，再在需要的端pull && push协同编辑即可，大致如下图
![flow](http://phiky9lnw.bkt.clouddn.com/flow.jpeg)
纯手绘，大致意思明白就好
