---
layout: mypost
title: 又又又换了博客的评论系统，也把软路由从R2S换成了R2S
categories: [tiwkoo,cusdis,waline]
---
#### 更换cusdis为twikoo
之前一直用的cusdis评论系统，之前的文章中也提到过。
- [博客添加文章评论系统cusdis](https://www.zahui.top/posts/2023/05/28/cusdis.html)
- [cusdis博客评论系统开始收费](https://www.zahui.top/posts/2023/08/23/cusdis-pay.html)

虽然cusdis收费之后，使用免费版对于小博主没有什么大的影响。但是评论被自动折叠，不支持跟随系统的夜间模式，还有最重要的，不能填写来访者的博客地址，这个一直是一个缺失。所以问了一下deepseek，如果想更换博客的评论系统，最重要的不需要实名认证，deepseek推荐的是wiekoo。

部署使用的是MongoDB+netlify+前端CDN引入的方式。记录一下遇到的问题
- fork了twikoo项目之后，在netlify的中看不到，点击：Can’t see your repo here? 然后Configure the Netlify app on GitHub.Repository access.这里需要做一个授权：All repositoriesThis applies to all current and future repositories owned by the resource owner. Also includes public repositories (read-only).所有仓库。这适用于资源所有者拥有的所有当前和未来仓库。还包括公共仓库（只读）。
- 添加云函数变量长链：mongodb+srv://<my_name>:<my_password>@cluster0.xxx.mongodb.net/xxx  这里面的<my_name>:<my_password>，是都不需要<> 的。
- netlify添加mongoDB变量长链的入口，和twikoo官网的位置不一致，应该是netlify的页面有改版，入口在site configuration-Environment variables
- 最重要的添加云函数变量之后，要刷新部署一下仓库。Deploys-Deploy site，否则云函数是不会生效的。
- 在获取邮件通知的时候，以为foxmail和qq是一家，虽然foxmail被QQ收购了，但是设置邮件通知，还是建议smtp server选择qq，使用qq邮箱最为简便，foxmail一直不能成功。

欢迎大家评论。

#### 更换软路由R2S为R4S
另外之前的软路由R2S感觉不能满足要求的，主要满足是docker的应用，所有从咸鱼买了一个R4S，使用istoreOS。更换软路由需要注意
- 之前用的拨号链接，拨号账号密码不要忘记，提前确认
- 选择tf卡时，比较重要的看这个tf卡的4k读写能力，从网上搜索了一下评测，买了金士顿的SDCG3。目前使用稳定，就算再docker里部署了Ubuntu，使用也算流畅。
- transmission、种子和lucky大吉。这里要注意，导入种子时，如果多块硬盘，先将要导入的硬盘设置为transmission的默认下载盘，这样不容易出错。lucky建议选择stun穿透51413，到软路由ip:51413
- 做好zerotier的准备
