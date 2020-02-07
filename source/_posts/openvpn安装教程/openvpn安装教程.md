---
layout: openvpn
title: openvpn安装教程
date: 2020-02-07 17:43:15
tags:
---
一、安装
1.[安装链接](https://github.com/Nyr/openvpn-install);
>安装或者添加一个用户
```shell
wget https://git.io/vpn -O openvpn-install.sh && bash openvpn-install.sh
```
>安装位置默认在/etc/openvpn/,配置文件为/etc/openvpn/server/server.conf;

代码片段
```code
local 172.17.0.11
port 1194
proto tcp
dev tun
ca ca.crt
cert server.crt
key server.key
dh dh.pem
auth SHA512
tls-crypt tc.key
topology subnet
server 10.8.0.0 255.255.255.0
ifconfig-pool-persist ipp.txt
push "redirect-gateway def1 bypass-dhcp"
push "dhcp-option DNS 183.60.83.19"
push "dhcp-option DNS 183.60.82.98"
keepalive 10 120
cipher AES-256-CBC
user nobody
group nobody
persist-key
persist-tun
status openvpn-status.log
verb 3
crl-verify crl.pem
```
二、[下载客服端](https://openvpn.net/);
三、服务器中启动关闭openvpn;

| 命令 | 作用 |
| -- | -- |
|开机启动|systemctl enable openvpn@server|
|启动|systemctl start openvpn@server|
|关闭 | start openvpn@server|
|查看状态|netstat -ano | grep 1194|

四、MAC客户端配置

1.软件下载地址:[https://tunnelblick.net/](https://tunnelblick.net/)
2、本地需要五个文件（三个用户名字开头的文件，一个ca.crt，一个认证文件.opvn)
3、从服务器上根据用户生成认证文件，打开Tunnelblick程序，把openvpn认证文件client.ovpn拖入到Tunnelblick程序配置列。(直接双击.openvpn文件)
4、点击连接即可，连接成功如下
