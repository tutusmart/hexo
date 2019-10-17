title: Centos下部署Nginx前端项目
author: Tutu
tags:
  - Centos
  - Linux
category:
  - Linux
categories:
  - Linux
date: 2019-10-12 14:50:00
---
### 一、下载
centos7 直接只用
```
yum install -y nginx
```
### 二、使用
找到nginx安装位置，我的安装位置在/etc/nginx
![](/images/pasted-2.png)
其中配置文件（nginx.config），我们可以指定端口 代理配置内容

### 三、 启动
CentOS 7.5下启动 Nginx 出现如下错误：
```shell
nginx: [error] open() "/run/nginx.pid" failed (2: No such file or directory)
```
解决方法：找到你的nginx.conf的文件夹目录，然后运行类似如下命令

### 四、代理
代理截图

![](/images/pasted-1.png)
```shell
nginx -c etc/nginx/nginx.conf
```
再运行
```shell
nginx -s reload
```

![](https://user-gold-cdn.xitu.io/2019/9/3/16cf6091d086ffc4?w=549&h=594&f=png&s=39516)

server下是配置内容 listen是具体的代理端口
server_name 是本地访问的端口这里项目启动的方式决定了我们代理的端口我们使用ip访问就需要配置一下这里的地址
location /api 就是指对应的前端访问的代理
例如

![](https://user-gold-cdn.xitu.io/2019/9/3/16cf60700837f339?w=782&h=269&f=png&s=27147)
我们访问的地址是 http://192.168.8.88/api/ 就会被代理到 http://sj.com/api

当然代理也可以配置多个如下：

![](https://user-gold-cdn.xitu.io/2019/9/3/16cf610242204d16?w=640&h=611&f=png&s=39254)
### 五、nginx 常用命令
|||
| -- | - |
|nginx -s stop  |   快速关闭Nginx，可能不保存相关信息，并迅速终止web服务。|
|nginx -s quit  |   平稳关闭Nginx，保存相关信息，有安排的结束web服务。|
|nginx -s reload |   因改变了Nginx相关配置，需要重新加载配置而重载。|
|nginx -s reopen |   重新打开日志文件。|
|nginx -c filename |  为 Nginx 指定一个配置文件，来代替缺省的。|
|nginx -t | 不运行，而仅仅测试配置文件。nginx将检查配置文件的语法的正确性，并尝试打开配置文件中所引用到的文件。|
|nginx -v        |    显示 nginx 的版本。|
|nginx -V        |   显示 nginx 的版本，编译器版本和配置参数。|