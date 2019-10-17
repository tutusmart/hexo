---
layout: '[centos安装git]'
title: centos安装git
date: 2019-10-16 15:54:37
tags:
    - Linux
categories:
    - Linux
---
一、获得一台linux服务器
要在linux下安装git，首先你得先有一台linux服务器，作为小白，手头的机器肯定都是windows的，搞个虚拟机安装对我这种小白简直是折磨人；这里使用最简单的方式获得一台linux服务器，就是从阿里云上租一台。镜像选择CentOS7.3 64位。

阿里云上租服务器
二、yum安装git
在linux上使用yum安装git非常简单，只需要一行命令

yum install git
随后就可以看到系统开始自动下载安装


yum安装git开始下载

出现提示是否下载的时候输入y并按回车。

yum安装git完成
输入git --version检查git是否安全完成，以及查看其版本号。
顺便说一下，yum安装git被安装在/usr/libexec/git-core目录下。


校验yum安装git
至此，yum安装git完成。

二、从github上下载最新的源码编译后安装git
yum安装这么简单，为什么还要学从github上下载最新的源码编译后安装呢？
刚才输入git --version命令的时候相信大家也看到了，是1.8.3.1版本，这个版本还是蛮旧的。yum安装就是这个缺点，版本你不好控制。如果想要使用最新版的git，那还是得自己下载源码安装。具体怎么做呢？

我们还是从一个什么都没安装的linux服务器开始示范。

1.进入git在github上的发布版本页面https://github.com/git/git/releases。在这个页面我们可以找到所有git已发布的版本。这里我们选择最新版的tar.gz包。


git在github上的仓库
2.获取到最新包的下载链接后，我们进入linux服务器，开始下载。

wget https://codeload.github.com/git/git/tar.gz/v2.13.0-rc1
耐心等待下载完成。我们可以看到下载后的文件名是v2.13.0-rc1，并不是压缩包的格式，不用担心，这只是链接的问题，手动修改文件名为v2.13.0-rc1.tar.gz。

mv v2.13.0-rc1 v2.13.0-rc1.tar.gz

下载git源码
解压压缩包

tar -zxvf v2.13.0-rc1.tar.gz
进入解压后的文件夹

cd git-2.13.0-rc1

源码解压完成
3.拿到解压后的源码以后我们需要编译源码了，不过在此之前需要安装编译所需要的依赖。输入如下命令。

yum install curl-devel expat-devel gettext-devel openssl-devel zlib-devel gcc perl-ExtUtils-MakeMaker
耐心等待安装完成，中途出现提示的时候输入y并按回车。


编译源码依赖安装完成
4.提示，安装编译源码所需依赖的时候，yum自动帮你安装了git，这时候你需要先卸载这个旧版的git。

yum remove git
耐心等待删除完成，中途出现提示的时候输入y并按回车。


移除旧版git
5.编译git源码

make prefix=/usr/local/git all
耐心等待编译完成，中途可能会花费几分钟的时间。


git源码编译完成
6.安装git至/usr/local/git路径

make prefix=/usr/local/git install
等待安装完成


git安装完成
7.打开环境变量配置文件

vim /etc/profile
在底部加上git相关配置

PATH=$PATH:/usr/local/git/bin
export PATH

修改环境变量
刷新环境变量

source /etc/profile
8.输入git --version检查git是否安全完成，以及查看其版本号。