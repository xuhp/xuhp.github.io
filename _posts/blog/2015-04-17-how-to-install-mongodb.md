---
layout:     post
title:      MongoDB安装教程（window版）
category:   blog
tags :      [ node, MongoDB]
description: MongoDban安装教程（window版）
---

##1. 下载
在mongodb官网（http://www.mongodb.org/downloads ) 下载安装包。 

![下载地址](https://raw.githubusercontent.com/xuhp/xuhp.github.io/master/images/howToInstallMongoDB/01.png)

我们在此选择windows的zip版本。（也可以选择MSI版本）

##2. 解压
解压到特定的目录下 。例如： F:/mongodb 

##3. 创建数据库文件的存放位置

例如：F:/mongodb/data/db

![数据库文件存放位置](https://raw.githubusercontent.com/xuhp/xuhp.github.io/master/images/howToInstallMongoDB/02.png)

也可以通过window的资源管理器创建这些目录。

启动mongodb服务之前必须要创建数据库文件的存放目录，否则命令不会自己主动创建，并且不能启动成功。默认目录路径为c:data/db，使用系统默认目录路径时，启动服务无需加--dbpath参数说明，但目录还要手工创建。

##4. 启动mongodb服务

打开cmd命令行，进入F:/mongodb/bin文件夹

mongod.exe --dbpath F:/mongodb/data/db

![启动mongodb服务](https://raw.githubusercontent.com/xuhp/xuhp.github.io/master/images/howToInstallMongoDB/03.png)

此时访问 http://localhost:27017/

![在浏览器中访问](https://raw.githubusercontent.com/xuhp/xuhp.github.io/master/images/howToInstallMongoDB/04.png)

##5. 将MongoDB服务器作为Windows服务器运行
这样每次启动都非常不方便，

请注意，你必须有**管理员权限**才能运行下面的命令。执行以下命令将MongoDB服务器作为Windows服务运行：

```cpp
mongod --bind_ip yourIPadress --logpath "C:\data\dbConf\mongodb.log" --logappend --dbpath "C:\data\db" --port yourPortNumber --serviceName "YourServiceName" --serviceDisplayName "YourServiceName" --install
```
![mongodb启动参数说明](https://raw.githubusercontent.com/xuhp/xuhp.github.io/master/images/howToInstallMongoDB/05.png)


例如：

```cpp
F:\mongodb\bin>mongod --logpath "F:\mongodb\logs\mongodb.log" --logappend --dbpath "F:\mongodb\data\db" --serviceName "MongoDB" --install
```

最后是安装參数：--install，与之相对的是--remove
以后就能够在cmd下用命令net start MongoDB和net stop MongoDB来启动和停止MongoDB了，也能够在本地服务中看到通过界面来管理该服务。

如何打开本地服务管理器  WIN+R   services.msc


##6. mongodb后台管理shell
MongoDB Shell 是MongoDB自带的交换式 Javascript shell ，用来对MongoDB进行操作和管理的交互式环境。

当你进入到MongoDB后台后，他会默认链接到test文档（数据）
可以运行简单的算术运算
db命令可以显示当前操作的文档
插入一些简单的记录并查找


![mongodb后台管理shell](https://raw.githubusercontent.com/xuhp/xuhp.github.io/master/images/howToInstallMongoDB/06.png)


##7. 参考文章

[MongoDB在window下的安装](http://www.cnblogs.com/mfrbuaa/p/4262883.html)

[window平台安装 MongoDB](http://www.w3cschool.cc/mongodb/mongodb-window-install.html)

[Windows8.1下安装NoSQL-- mongodb安装使用](http://www.cnblogs.com/angelasp/p/4323636.html)



















