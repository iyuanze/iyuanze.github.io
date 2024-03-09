---
layout: mypost
title: RSS站readdig.com开始收费了,自建RSS服务
categories: [readdig,RSS,RSS源,TinyTinyRSS,FreshRSS]
---

常用的RSS站点是今日热点tophub.today，每天上班的摸鱼时间快速了解当前热点。

另外一个就是自己通过 readdig.com 自己订阅的RSS。readdig非常便捷的，最实用的就是：不用科学场景，就可以了解外站的RSS。

最近打开readdig的时候，发现已经收费了。一直以来RSS服务的盈利就是一个未能解决的问题，不知道readdig付费的情况怎么样。目前收费的标准是US2.99/month，按照2024年3月9日汇率计算，大概21.5元RMB/月，215元RMB/年。这个收费标准，嗯……。

![image](https://www.wuyeso.com/i/zb_users/upload/2024/03/202403091709993251708970.png)

#### # 选择RSS服务程序
搜索了一下如果自建RSS服务的话，推荐的比较多的还是Tiny Tiny RSS和FreshRSS。目前还有一个bluehost的虚拟主机在续费，准备自建一个RSS服务。

- Tiny Tiny RSS 官网：[Tiny Tiny RSS (tt-rss.org) 官网](https://tt-rss.org/)。

- FreshRSS 官网： [FreshRSS, a free, self-hostable feeds aggregator](https://www.freshrss.org/)

对比下来FreshRSS安装更简单，可以用虚拟主机。原计划官网下载安装包，虚拟主机安装。后来想到bluthost有softaculous服务。Tiny Tiny RSS更新事件2019年8月，FreshRSS更新时间2023年12月。毫无疑问选择FreshRSS。

![image](https://www.wuyeso.com/i/zb_users/upload/2024/03/202403091709994372369609.png)

![image](https://www.wuyeso.com/i/zb_users/upload/2024/03/202403091709994474205294.png)


#### # 安装
快捷安装，2分钟完成。配置域名，记住账户密码。

![image](https://www.wuyeso.com/i/zb_users/upload/2024/03/202403091709994591646807.png)

#### # RSS源

然后，问题来了。RSS源哪里找？特别是免翻的RSS源。readdig之前订阅了很多的RSS，去看了一下，有个导出OPML，导出后HTML打开。其中xmlUrl=""这个里面就是订阅地址。在FreshRSS进行配置就可以了，有些源已经失效了，大部分还可以使用。

![image](https://www.wuyeso.com/i/zb_users/upload/2024/03/202403091709994803242480.png)

#### # 安装完成

![image](https://www.wuyeso.com/i/zb_users/upload/2024/03/202403091709995756810885.png)
