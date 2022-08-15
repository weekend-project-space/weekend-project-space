+++
author = "瑞东"
title = "rss read 上线了 (webfollow1.5)"
date = "2022-08-15"
description = "rss2reader"
tags = [
    "网站",
    "周末项目"
]
categories = [
    "project",
]

+++

- 开发用时:20小时+
- 费用:0元+

webfollow.cc 上线一周后积累了20个用户，由于上手门槛还是过于高，于是就有了 webfollow 的阅读版 (更易上手，所见即所得 read模式), 之前rss2letter转移到了 [webfollow.cc/watch](http://webfollow.cc/watch) 下


##  网站介绍

![webfollow-rss-reader](/images/webfollow-1.5/index.jpg)

页面分成了三块 

- 首页 ： 用户订阅信息的聚合
- 探索 ： 不只是用户订阅的内容，还有更多相关的频道和信息
- 订阅 ： 管理订阅的rss可以方便快速的查看该rss频道下的内容

后台继续采用了webfollow-rss2letter 的后台, 前台采用vue+vite+pwa技术栈开发，用时2天多一点。


## 关于开发的一些想法

- 首页推荐和探索模块打算结合点击做一下排名优化，算法还在设计中；
- 目前订阅功能只支持系统初始化的的rss源，无法让用户自己订阅自己喜欢的源，这也是下一步要开发的功能;
- webfollow第一版倾向于为用户过滤信息提供 if someting notice me,由于前面提到的原因于是有了更简单的所见及所得的read模式，不过并不意味着第一版中的 isnm 的方式就弃用了。

## 碎碎念

写软件做产品对于一个程序员来说相对简单些，渠道分发这一块的知识则多是空白的，之前看到[alax](https://www.alexwest.co/)的博客上有这么一句话作为结尾。

> 如果我要留给你一句话，那就是：请记住，在您找到产品/渠道/系统组合后，事情会变得更容易。而且您不必多次找到它。就一次。所以不要因为你还没有找到它就放弃。


