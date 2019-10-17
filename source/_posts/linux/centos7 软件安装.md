title: centos7 软件安装
tags:
  - Centos
  - Linux
category:
  - Linux
date: 2019-10-11 19:29:40
---
### 1.安装Mysql
在要安装的目录下执行一下命令 我这就是进入到/home/money/后执行以下命令

下载
```shell
wget -i -c http://dev.mysql.com/get/mysql57-community-release-el7-10.noarch.rpm
```
yum 安装
```shell
yum -y install mysql57-community-release-el7-10.noarch.rpm
```
安装mysql服务器
```shell
 yum -y install mysql-community-server
```
起动mysql服务器
```shell
systemctl start mysqld
```
修改密码

    第一次安装会给root随机密码 查看 grep "password" /var/log/mysqld.log
    进入数据库 mysql -uroot -p密码
    修改密码 ALTER USER 'root'@'localhost' IDENTIFIED BY '你要设置的密码';
    (要包含大小写和符号，比较难设置)

修改mysql语言

    首先重新登录mysql，然后输入status：
    此处语言并不是utf8,我们退出（输入exit）去修改
    
![upload successful](/images/pasted-7.png)

    vi /etc/my.cnf
    复制代码添加四行代码

![upload successful](/images/pasted-6.png)

重启mysql服务,登录后status查看，改成utf8就成功了
shell service mysqld restart
操作命令：
启动mysql服务 service mysqld start 重启mysql服务 service mysqld restart 查看状态服务状态 service mysqld status