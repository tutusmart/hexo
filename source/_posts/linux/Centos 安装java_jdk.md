title: Centos 安装java_jdk
tags:
  - Linux
categories:
  - Linux
date: 2019-11-28 20:04:00
---
### 1、先查看centos中自带的jdk并卸载

![upload successful](/blogs/images/pasted-26.png)

### 2、yum 命令查找jdk  两种方法：
1.yum -y list java*

![upload successful](/blogs/images/pasted-27.png)

2.yum search jdk
![upload successful](/blogs/images/pasted-28.png)

### 3丶安装jdk  作者安装  java-1.8.0-openjdk.x86_64
3.yum install java-1.8.0-openjdk.x86_64

![upload successful](/blogs/images/pasted-29.png)

### 4、检验安装

![upload successful](/blogs/images/pasted-30.png)

### 5、yum 命令安装默认安装路径为 /usr/lib/jvm


![upload successful](/blogs/images/pasted-31.png)

### 6、设置jdk环境变量

```shell
vim /etc/profile
```
在文件最后加入如下配置：
```shell
#set java environment
JAVA_HOME=/usr/lib/jvm/jre-1.8.0-openjdk.x86_64
PATH=$PATH:$JAVA_HOME/bin
CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
export JAVA_HOME CLASSPATH PATH
```
### 7、使profile文件立马生效

![upload successful](/blogs/images/pasted-32.png)


