---
layout: mypost
title:  macos批量保存html网页中的图片
categories: [macos,macmini,批量保存]
---

> 跟风买了mac mini 对于macos的使用，需要适应和学习

#### #背景：批量保存网页中图片的需求

PT站老师最近一期的趣味盒的图片特别顶。safari浏览器，将网址中的/index.php，修改为fun.php，可以进去趣味盒的专属页面。图片大小在5m左右，使用的第三方图床iili.io，加载的比较慢，加载完成可以右键保存。

因为本期的图片数量比较多，每一张右键保存比较慢。所以想用python批量保存。问了一下豆包，给出了方案：
##### 方案一：python直接引用需要下载图片的网址下载

下载失败，仅仅下载到了html页面中的按钮图标的图片。

##### 方案二：网页采用动态加载，需要调用Selenium

再次询问豆包，表示遇到的问题是网页采用动态加载（比如 JavaScript 异步加载图片），普通的requests只能获取初始 HTML，无法等待动态内容加载完成，所以需要改用能模拟浏览器渲染页面的工具 ——Selenium，它可以像真人一样等待页面加载完毕后再解析图片。但是这种方式就比较复杂了。

##### 方案三：保存html文件，通过本地保存的html文件保存图片

第三次询问豆包，页面已经加载完成，有没有办法直接通过加载完成的页面直接下载。豆包建议保存为html文件，再保存下载图片。

safari浏览器➡️文件➡️保存为➡️，有三个选项：页面源码，页面归档，PNG。选择页面源码，保存的是html文件，但是只是快捷方式，已经加载的图片位包含。

选择页面归档，保存的是.webarchive文件，在webarchive文件中是包含了已经加载的图片的。所以豆包提供的通过保存的html文件，不成立。

##### 方案四：通过webarchive文件获取图片

第四次询问豆包，告知了webarchive文件中包含了图片。豆包首先提供的方案是通过python下载已经保存到本地了webarchive文件，下载成功，但是下载文件为0。

反馈了这个问题之后，豆包给出反馈：

> 这是因为 Safari 保存的 webarchive 结构有两种，我上一版代码只覆盖了一种，没命中你这种。我现在直接给你100% 能提取出图片的最简单、最稳的方案，不用改代码、不用猜结构，你现在就能用。

给出了最终方案：把 webarchive 转成文件夹（自动拆出所有图片）。需要用到的工具是textutil，并且进行了解释说明。

- textutil 是 Mac 自带工具，苹果自己写的
- 它完美解析 Safari webarchive
- 它会把 webarchive 自动拆成网页 + 全部图片
- 不管图片是哪种结构，全部能拆出来
- 你之前代码提取 0 张，是因为 webarchive 内部结构有很多变种，但 textutil 是官方解析器，不会漏。

#### #总结：macos系统safari浏览器批量保存网页中图片的最简方案

通过textutil工具。

```
# 核心修正：-output 指定「文件夹+HTML文件名」，而非直接写文件夹
textutil -convert html "/Users/用户名/Desktop/nicept_fun.webarchive" -output "/Users/用户名/Desktop/fun/nicept_fun.html"
```

#### 需要注意的问题：
1. 如果用macOS的文本编辑，进行编辑python文件，需要先在文本编辑➡️设置➡️新建文稿➡️选择纯文本，系统默认的多信息文本，就算后缀改成了.py，python调用的时候也会出错。
2. 网页可以直接保存为pdf，如果不是必须保存为图片，只是为了收藏，pdf也许是更好的选择。
3. 加载完成的网页保存为webarchive，使用textutil工具时，在桌面建立了文件夹，output不能直接写文件夹。
4. textutil的-output参数规则：
    - 转换 WebArchive 到 HTML 时，-output后必须指定具体的 HTML 文件名（比如fun/nicept_fun.html）；
    - 工具会自动在该 HTML 文件同目录下创建XXX_files文件夹，把所有图片 / 资源放进这个文件夹，而非直接散放。
  
![2026-03-08-14-43-24.avif](https://user0118.cn.imgto.link/public/20260308/2026-03-08-14-43-24.avif)
