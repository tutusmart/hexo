title: Win10安装Mongodb，并配置成服务
author: Tutu
date: 2019-10-14 09:49:07
tags:
  - win10
category:
  - mongodb
---
### 一：下载安装，然后拷贝到C盘根目录，这个就不多说了，比QQ都简单。

### 二：把bin文件夹拷贝到跟MongoDB目录，然后在根目录下建一个data文件夹存放日志跟数据库，然后data文件夹下建db跟log文件夹，并在log文件夹下新建一个日志文件mongolog.log，如下

图所示：
![](https://user-gold-cdn.xitu.io/2019/8/6/16c659090f8ce681?w=516&h=304&f=png&s=17920)![](https://user-gold-cdn.xitu.io/2019/8/6/16c6590c733468f9?w=567&h=244&f=png&s=14427)![](https://user-gold-cdn.xitu.io/2019/8/6/16c6590f19426cd6?w=635&h=226&f=png&s=14108)

### 三：在mongodb根目录下见一个配置文件，内容如下：
```txt
dbpath=c:\MongoDb\data\db
logpath=c:\MongoDB\data\log\mongolog.log
logappend=true
auth=false
```
这就是mongodb.config文件的内容，auth默认为false，不起用密码验证

### 四：powershell管理员模式定位到bin目录，然后运行

```shell
.\mongod --config c:\MongoDB\mongodb.config --serviceName MongoDB --install
```

 这样，服务就安装完了，然后在服务那块右键启动服务，这样mongodb就算安装好了，接下来要设置密码

### 五.当mongod.exe被关闭时，mongo.exe 就无法连接到数据库了，因此每次想使用mongodb数据库都要开启mongod.exe程序，所以比较麻烦，此时我们可以将MongoDB安装为windows服务

　还是运行cmd，进入bin文件夹，执行下列命令
```shell
> d:\mongodb\bin>mongod --dbpath "d:\mongodb\data\db" --logpath "d:\mongodb\data\log\MongoDB.log"
  --install --serviceName "MongoDB"
```


这里MongoDB.log就是开始建立的日志文件，--serviceName "MongoDB" 服务名为MongoDB
接着启动mongodb服务

### 六.关闭服务和删除进程
```shell
> d:\mongodb\bin>NET stop MongoDB   (关闭服务)
> d:\mongodb\bin>mongod --dbpath "d:\mongodb\data\db" --logpath "d:\mongodb\data\log\MongoDB.log" --remove --serviceName "MongoDB"
```
>(删除，注意不是--install了)