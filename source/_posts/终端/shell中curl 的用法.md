title: shell中curl 的用法
author: Tutu
tags:
  - shell
categories:
  - shell
date: 2019-10-14 14:32:00
---
curl 是常用的命令行工具，用来请求 Web 服务器。它的名字就是客户端（client）的 URL 工具的意思。

它的功能非常强大，命令行参数多达几十种。如果熟练的话，完全可以取代 Postman 这一类的图形界面工具。

### 1.不带有任何参数时，curl 就是发出 GET 请求。
```shell
curl https://www.example.com
```
![](https://user-gold-cdn.xitu.io/2019/9/19/16d495a71b078a30?w=1414&h=216&f=png&s=70212)

### 2.-b参数用来向服务器发送 Cookie。
```shell
$ curl -b 'foo=bar' https://google.com
```
上面命令会生成一个标头Cookie: foo=bar，向服务器发送一个名为foo、值为bar的 Cookie。
```shell
$ curl -b 'foo1=bar' -b 'foo2=baz' https://google.com
```
上面命令发送两个 Cookie。
```shell
 curl -b cookies.txt https://www.google.com
 ```
 上面命令读取本地文件cookies.txt，里面是服务器设置的 Cookie（参见-c参数），将其发送到服务器。


  ### -c
  参数将服务器设置的 Cookie 写入一个文件。
 ```shell
 $ curl -c cookies.txt https://www.google.com
 ```
 上面命令将服务器的 HTTP 回应所设置 Cookie 写入文本文件cookies.txt。
  ### -d
  参数用于发送 POST 请求的数据体。
 ```shell
$ curl -d 'login=emma＆password=123'-X POST https://google.com/login
# 或者
$ curl -d 'login=emma' -d 'password=123' -X POST  https://google.com/login
```
使用-d参数以后，HTTP 请求会自动加上标头Content-Type : application/x-www-form-urlencoded。并且会自动将请求转为 POST 方法，因此可以省略-X POST。

-d参数可以读取本地文本文件的数据，向服务器发送。
```shell
$ curl -d '@data.txt' https://google.com/login
```
上面命令读取data.txt文件的内容，作为数据体向服务器发送。