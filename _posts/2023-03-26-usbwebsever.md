***

layout: mypost
title:  使用U盘搭建Web本地服务器，安装zblog
categories: \[usbwebserver,zblog,U盘服务器]
---------------------------------------

周末在[十年之约foreverblg专题展示](https://www.foreverblog.cn/feeds.html) 看看加入十年之约的博客rss。看到了一篇文章，讲到了使用U盘搭建Web本地服务器。博主说到，有了随身携带可编辑，并且不对外展示的个人博客的需求。虽然本人目前没有这样的需求，但是尝试了一下，这个usbwebsever搭建起来确实非常方便，安装zblog测试一下，没有任何报错。

#### # usbwebsever实战搭建

##### 1、先期准备

U盘一个

下载：[USBWebserver](https://usbwebserver.yura.mk.ua/)

软件介绍： USBWebserver 自带Apache、PHP、MySQL 和 PHPMyAdmin，只需解压缩到U盘里，运行并开始使用即可。

##### 2、使用简述：

下载并解压 USBWebserver 到 U 盘或本地。

打开解压好的文件夹并运行 usbwebserver.exe

首次启动 USBWebServer 时选择您的语言（打开软件，选择 Setting –>Language –>Chinese ），如果与其他本地 Web 服务器端口冲突，可更改默认端口。

站点根目录路径：<http://localhost>

##### 3、管理员账户：

PhpMyAdmin 设置：

默认数据库名：test

用户名：root

密码：usbw

PhpMyAdmin 访问路径：<http://localhost/phpmyadmin>

#### # usbwebserver安装zblog

采用便捷的zblog在线安装方式：

[Z-BlogPHP在线安装程序](https://www.zblogcn.com/zblogphp/)

下载单文件：[install.php](https://update.zblogcn.com/onlinephp/install.zip)

放置在ROOTdir根目录，如果不知道这个目录在哪里，可以点击这里打开：

![rootdir](https://www.wuyeso.com/zb_users/upload/2023/03/202303261679826831291317.png)

访问地址：<http://localhost/install.php，就可以在线安装（电脑需要有网络），数据库用户名，账号密码均按照上述说明填写即可。>

#### # 拓展下载

USBWebServer ：<https://usbwebserver.yura.mk.ua/>

#### # 推荐zblog免费主题

推荐一个zlog主题，如果是自己随身携带的usbwebsever服务器，那么推荐一个响应式帮助中心主题/知识库主题。

这个主题类似官网的帮助中心，或者说知识库，帮助自己整理资料，梳理自己的知识框架。

主题地址：[响应式帮助中心主题](http://localhost/zb_users/plugin/AppCentre/main.php?id=8316)

上面的网址需要你安装好了zblog，在应用中心里面搜索帮助中心即可。如果你还未安装，需要查看一下效果，可以参考下面的网站：

主题效果参考：[物业帮助中心](https://www.wuyeso.com/help/) <https://www.wuyeso.com/help/>

![响应式帮助中心](https://www.wuyeso.com/zb_users/upload/2023/03/202303261679828069591394.png)

> 参考文章：<https://blog.xzbzq.com/3806.html>

