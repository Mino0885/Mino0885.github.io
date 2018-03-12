---
layout: page
title: About
description: Mino的github
keywords: Mino, Mino0885
comments: true
menu: 关于
permalink: /about/
---
## 关于我

90后程序员的血泪史 (；´д｀)ゞ

愿我爱的人和爱我的人远离 bug ( • ̀ω•́ )

精通IDEA开发工具

熟练使用SSH SSM 框架 (详情见简历)

## Skill Keywords

{% for category in site.data.skills %}
##### {{ category.name }}
<div class="btn-inline">
{% for keyword in category.keywords %}
<button class="btn btn-outline" type="button">{{ keyword }}</button>
{% endfor %}
</div>
{% endfor %}
