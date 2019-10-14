title: SSH 上传下载文件
author: Tutu
date: 2019-10-14 09:46:01
tags:
  - Centos
  - Linux
category:
  - Linux
---
### 1、上传本地文件到服务器
```shell
    scp /path/filename username@servername:/path/
```
例如scp /var/www/test.php root@192.168.0.101:/var/www/ 把本机/var/www/目录下的test.php文件上传到192.168.0.101这台服务器上的/var/www/目录中

### 2、从服务器上下载文件
下载文件我们经常使用wget，但是如果没有http服务，如何从服务器上下载文件呢？
```shell
scp username@servername:/path/filename /var/www/local_dir（本地目录）
```
例如scp root@192.168.0.101:/var/www/test.txt 把192.168.0.101上的/var/www/test.txt 的文件下载到/var/www/local_dir（本地目录）

### 3、从服务器下载整个目录
```shell
scp -r username@servername:/var/www/remote_dir/（远程目录） /var/www/local_dir（本地目录）
```
例如:scp -r root@192.168.0.101:/var/www/test /var/www/

### 4、上传目录到服务器
```shell
scp -r local_dir username@servername:remote_dir
```
例如：scp -r ui root@192.168.8.88:/var/share/nginx/ (ui 桌面文件，/var/share/nginx/远程文件 );
>上传的时候应该断开连接SSH 会提示输入密码