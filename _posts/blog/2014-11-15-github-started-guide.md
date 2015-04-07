---
layout:     post
title:      github新手指南
category: blog
tags : [ git ,静态博客,主题]
description: git是分布式的版本控制系统，和svn的概念同级。GitHub (https://github.com)  是一个面向开源及私有软件项目的托管平台，因为只支持Git作为唯一的版本库格式进行托管，故名GitHub。
---

git是分布式的版本控制系统，和svn的概念同级。

GitHub (https://github.com)  是一个面向开源及私有软件项目的托管平台，因为只支持Git作为唯一的版本库格式进行托管，故名GitHub。

>http://www.imooc.com/learn/208

##1. 注册github账号

首先登陆 https://github.com 注册github账号

## 2. 安装git
 
>只讲解git在window下的配置

1. 从git官网下载windows版本的git: [http://git-scm.com/downloads](http://git-scm.com/downloads)

2. 一般使用默认设置即可：一路next,git安装完毕！

3. 但是如果这个时候打开windows的cmd,在里面打开git命令会提示“不是内部或外部命令，也不是可运行程序”，想要直接在windows的cmd里使用git命令要多加两步

4. 找到git安装路径中bin的位置，如：C:\Program Files\Git\bin.  找到git安装路径中git-core的位置，如：C:\Program Files\Git\libexec\git-core

5. 右键“计算机” -> “属性” -> "高级系统设置" -> “环境变量” -> 在系统变量中找到"path" -> 选中"PATH"并选择“编辑” -> 将4中找到的bin和git-core路径复制到其中 -> 保存并退出

> 注： “C:\Program Files\Git\bin”是安装路径，可能与你的安装路径不一样，要按照自己的路径替换“C:\Program Files\Git\bin”

> 注： “PATH”中，每个路径之间要以英文输入状态下的分号——“;”作为间隔

> 注： 环境变量分为系统环境变量和用户环境变量。系统环境变量，对所有用户起作用。用户环境变量只对当前用户起作用。

**git相关知识**

 git-简易指南 [http://www.bootcss.com/p/git-guide/](http://www.bootcss.com/p/git-guide/)
 
 Git使用基础 [http://www.open-open.com/lib/view/open1332904495999.html](http://www.open-open.com/lib/view/open1332904495999.html)

 Git Push 避免使用用户名和密码方法 [http://www.cnblogs.com/ballwql/p/3462104.html] [ http://blog.csdn.net/leejearl/article/details/38656713]

##3. 设置SSH建立计算机与github的链接

###3.1. 打开Git Bash

![打开git Bash](https://raw.githubusercontent.com/AsiaFE/weekly-meeting/master/%E8%B5%84%E6%BA%90%E5%BA%93/20141106/01.png)

###3.2. 运行命令cd ~/.ssh 检查自己的电脑上是否存在ssh keys

![](https://raw.githubusercontent.com/AsiaFE/weekly-meeting/master/%E8%B5%84%E6%BA%90%E5%BA%93/20141106/02.png)

如果显示No such file or directory 则需要去创建一个新的ssh keys

###3.3. 创建新的ssh keys 

运行命令：$ ssh-keygen -t rsa -C "your_email@youremail.com"  回车

![](https://raw.githubusercontent.com/AsiaFE/weekly-meeting/master/%E8%B5%84%E6%BA%90%E5%BA%93/20141106/03.png)

输入密码并重新确认

![](https://raw.githubusercontent.com/AsiaFE/weekly-meeting/master/%E8%B5%84%E6%BA%90%E5%BA%93/20141106/04.png)

 > 注：在Enter passphrase的时候，输入的密码是看不到的，其实已经输入，完成后点击回车就行了。

这样新的keys就创建完成了，上面代码显示，秘钥位置放在了/c/users/用户名/.ssh/文件夹中。（.ssh文件夹可能是隐藏的，需要查看隐藏文件）

###3.4 将生成的ssh keys添加到github中

Account Settings > SSh keys > Add ssh

![](https://raw.githubusercontent.com/AsiaFE/weekly-meeting/master/%E8%B5%84%E6%BA%90%E5%BA%93/20141106/05.png)

在本机找到你创建的密钥文件id_rsa.pub,使用记事本打开，复制所有的内容，粘贴到key文本框中，点击Add Key保存

###3.5 测试一下我们的设置是否正确

输入命令：$ ssh -T git@github.com

![](https://raw.githubusercontent.com/AsiaFE/weekly-meeting/master/%E8%B5%84%E6%BA%90%E5%BA%93/20141106/06.png)

输入yes

![](https://raw.githubusercontent.com/AsiaFE/weekly-meeting/master/%E8%B5%84%E6%BA%90%E5%BA%93/20141106/07.png)

本机显示连接关闭，继续执行 $ ssh -T git@github.com ，提示输入密码，输入密码。回车登陆成功。

> 如果SSH还是无法使计算机和github建立连接则可以参照如下文章 http://computer.uoh.edu.cn/android/526.html

##4 在本地设置Git信息

###4.1 设置用户名和邮箱

```cpp
  $ git config --global user.name "真实姓名"
  $ git config --global user.email  "your_email@youremail.com
```

此处用户名为自己的实际姓名，而非登陆用户名 

##5 创建一个库

###5.1 点击New repository

 ![](https://raw.githubusercontent.com/AsiaFE/weekly-meeting/master/%E8%B5%84%E6%BA%90%E5%BA%93/20141106/08.png)

**github clone文件**

git clone git://git.kernel.org/pub/scm/git/git.git

 ![](https://raw.githubusercontent.com/AsiaFE/weekly-meeting/master/%E8%B5%84%E6%BA%90%E5%BA%93/20141106/09.png)

**github 删除文件**

```cpp
  $ git commit -a -m "mesage"
  $ git push origin master
```






















