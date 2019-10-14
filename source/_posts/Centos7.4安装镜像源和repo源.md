title: Centos7.4安装镜像源和repo源
author: Tutu
date: 2019-10-14 09:48:34
tags:
---
### 一、国内可选下载镜像源
#### 1、国内  
163镜像源（推荐选择）  
http://mirrors.163.com/  
中国技术科学大学  
http://mirrors.ustc.edu.cn/  
Centos官方站点  
http://vault.centos.org/  
#### 2、Centos7.4下载地址
http://mirrors.163.com/centos/7.4.1708/isos/x86_64/CentOS-7-x86_64-DVD-1708.iso
### 二、配置Centos7.4的yum源
#### yum所需要使用的repo源如下：
在安装好的操作系统中，执行如下命令：
vim /etc/yum.repos.d/CentOS-163.repo
```shell
# geographically close to the client.  You should use this for CentOS updates
# unless you are manually picking other mirrors.
# 
# If the mirrorlist= does not work for you, as a fall back you can try the 
# remarked out baseurl= line instead.
#
# Jeson@imoocc.com
[base]
name=CentOS-$releasever - Base - 163.com
#mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os
baseurl=http://mirrors.163.com/centos/$releasever/os/$basearch/
gpgcheck=1
gpgkey=http://mirrors.163.com/centos/RPM-GPG-KEY-CentOS-7

#released updates
[updates]
name=CentOS-$releasever - Updates - 163.com
#mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates
baseurl=http://mirrors.163.com/centos/$releasever/updates/$basearch/
gpgcheck=1
gpgkey=http://mirrors.163.com/centos/RPM-GPG-KEY-CentOS-7

#additional packages that may be useful
[extras]
name=CentOS-$releasever - Extras - 163.com
#mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras
baseurl=http://mirrors.163.com/centos/$releasever/extras/$basearch/
gpgcheck=1
gpgkey=http://mirrors.163.com/centos/RPM-GPG-KEY-CentOS-7

#additional packages that extend functionality of existing packages
[centosplus]
name=CentOS-$releasever - Plus - 163.com
baseurl=http://mirrors.163.com/centos/$releasever/centosplus/$basearch/
gpgcheck=1
enabled=0
gpgkey=http://mirrors.163.com/centos/RPM-GPG-KEY-CentOS-7
```