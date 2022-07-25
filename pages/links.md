---
layout: mypost
title: 友情链接
---

欢迎各位朋友与我建立友链，如需友链请到[留言板](chat.html)留言，我看到留言后会添加上的，本站的友链信息如下

```
名称：涓滴意念汇成河
描述：一个大杂烩，走一程有一程的风景，进一步有一步的欢喜。
地址：[https://www.zahui.top/](https://www.zahui.top/)
头像：[https://www.zahui.top/static/img/logo.jpg](https://www.zahui.top/static/img/logo.jpg)
```

<ul>
  {%- for link in site.links %}
  <li>
    <p><a href="{{ link.url }}" title="{{ link.desc }}" target="_blank" >{{ link.title }}</a></p>
  </li>
  {%- endfor %}
</ul>
