title: VMWare 下安装Centos网络设置（局域网配置）
author: Tutu
tags:
  - vm
category:
  - Linux
date: 2019-10-14 09:46:57
---
**最近打算为centos安装一个界面时，发现不能上网。ping www.baidu.com 报name or service not known。
原来网络配置没设好。**

### 一、选择VMWare的NAT模式。
1）导航栏“编辑”->“虚拟网络编辑器” ->NAT模式->NAT设置
![](/blogs/images/1571319042.jpg)

>记住NAT设置中的子网IP、子网掩码、网关IP三项，接下来配置文件主要是这三项。
 嗯，这里记得按确定，我之前没有按确定写好配置后还是不行，不知道为什么。

### 二、编辑网络配置文件。

- 选择虚拟机桥接模式
- 编辑网卡设置文件
- 重启网卡

我的是ens33，不同的人或许会有不同。
```shell
vi /etc/sysconfig/network-scripts/ifcfg-ens33
```
我的是这样的。

![upload successful](/blogs/images/pasted-3.png)

打开配置文件后，按“i”进行编辑

![upload successful](/blogs/images/pasted-4.png)

更改完后，按“ESC”键，然后输入":wq"。意思是退出并保存。

```shell
service network restart
```
接下来就可以愉快的 ping www.baidu.com
![upload successful](/blogs/images/pasted-5.png)

>附文件代码
```shell
TYPE=Ethernet
BOOTPROTO=static  #启用静态IP地址
DEFROUTE=yes
PEERDNS=yes
PEERROUTES=yes
IPV4_FAILURE_FATAL=no
IPV6INIT=yes
IPV6_AUTOCONF=yes
IPV6_DEFROUTE=yes
IPV6_PEERDNS=yes
IPV6_PEERROUTES=yes
IPV6_FAILURE_FATAL=no
NAME=eno16777736
UUID=ae0965e7-22b9-45aa-8ec9-3f0a20a85d11
ONBOOT=yes  #开启自动启用网络连接
IPADDR=192.168.8.88  #设置IP地址
NETMASK=255.255.255.0  #设置子网掩码
GATEWAY=192.168.8.254  #设置网关
DNS1=192.168.1.2 #设置主DNS
DNS2=192.168.1.3 #设置备DNS
```