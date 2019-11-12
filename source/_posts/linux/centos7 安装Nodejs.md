title: centos7 安装Nodejs
tags:
  - Centos
  - Linux
category:
  - Linux
date: 2019-11-12 11:29:40
---
### 1、去官网下载和自己系统匹配的文件

下载
```shell
wget -i -c https://npm.taobao.org/mirrors/node/v12.13.0/node-v12.13.0-linux-x64.tar.xz
```
### 2、下载下来的tar文件上传到服务器并且解压，然后通过建立软连接变为全局；
1.查看文件路径：目前我的放置路径为`/usr/local/`
2.解压
```shell
tar -xvf   node-v6.10.0-linux-x64.tar.xz
mv node-v6.10.0-linux-x64  nodejs //修改文件名
```
3.确认一下nodejs下`bin`目录是否有`node` 和`npm`文件，如果有执行软连接，如果没有重新下载执行上边步骤；

### 3、建立软连接，变为全局
```shell
   ln -s /usr/local/nodejs/bin/npm /usr/local/bin/
   ln -s /usr/local/nodejs/bin/node /usr/local/bin/
```
### 4、修改配置文件，在 /etc/profile
1.修改内容
![upload successful](/images/pasted-23.png)

2.`source /etc/profile`

3.Linux命令行node -v 命令会显示nodejs版本