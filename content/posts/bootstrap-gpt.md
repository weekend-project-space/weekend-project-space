+++
author = "瑞东"
title = "Bootstrap GPT 是什么"
date = "2023-03-22"
description = "ChatGPT 联网后可以做什么"
tags = [
   "博客","GPT"
]
categories = [
    "blog",
]

+++

## 故事的开始

前些日子受 auto gpt 的启发，这次的输出当作下次的输入，想着能否将 prompts 当作一种编程的手段，而且让其支持联网 ，比如 写一个 ppt 或 文档 或总结网页内容 等等 让它去引导你，就像一个问卷调查 然后给你生成你需要的结果。

然后当天下午就写了一个出来是 cmd 的交互方式，验证成功

![bootstrap-gpt](https://raw.githubusercontent.com/weekend-project-space/bootstrap-gpt/main/doc/demo.gif)

后面在社区有人回复说网络的方式更好，然后就又增加了 http 的方式，这里有一个展示视频可以展示现在它能做的事情

![gpt-online](https://raw.githubusercontent.com/weekend-project-space/bootstrap-gpt/main/doc/gpt-online-demo.gif)

**这些是如何运作的？**

我们先通过 ls 命令会罗列出现在有那些功能:

ls

```
summarize : 总结网页
v2-hot : 查看v2最近热门帖子讲了什么
while : 循环次数测试
hot : 查看webfollow最近热门帖子讲了什么
friend : chat 聊天 引导助手
writecode : code boot
spider : wiki 引导助手
```

然后 使用 use summarize 这个功能作为演示， bootstarp-gpt 会加载 bootstarp 下的文件，这里有一个总结网页讲了什么的 summarize.json 文件

```json
{
  "author": "ruidong",
  "date": "2023-04-19",
  "version": "0.1",
  "description": "总结网页",
  "boot": [
    {
      "w": "请输入网址",
      "r": "r0",
      "p": "spider:{{r0}}:select=.entry-content p"
    },
    {
      "p": "chat:总结一下这个页面介绍了什么{{m0}}"
    },
    {
      "w": "总结: {{m1}} \n还要总结其他网页吗? y/n",
      "r": "r2",
      "b": {
        "y": 0,
        "n": -1
      }
    }
  ]
}
```

当使用 总结网页这个命令时 Bootstarp GPT 会加载这个文件运作，

- 控制台输出 请输入网址 ，
- 然后等待输入，
- 接着将输入的网址调用爬虫抓取，
- 抓取到的结果通过 chat 进行总结，
- 把总结的内容打印到控制台上，
- 最后等待输入是否继续总结其他网页
- 继续则跳转到第 1 条命令也就是下标是 0 的位置继续执行，否则退出

这些功能的开发都很简单，目前还只是玩具一样的小项目。

如果你对此感兴趣可以通过这里获取源码[bootstrap-gpt](https://github.com/weekend-project-space/bootstrap-gpt)

## 结尾

最后用总结功能让其总结了一下这篇文件讲了什么:

```
> use summmarize
请输入网址
> https://weekendproject.space/posts/bootstrap-gpt/

总结: 本页面介绍了 Bootstrap GPT，它是一个可以将 prompts 作为编程手段的工具，
并支持联网功能。通过展示视频和代码示例，介绍了如何使用 Bootstrap GPT 的各种功能，
主要包括总结网页、查看热门帖子、循环测试、聊天引导助手、代码编写、爬虫引导助手等，
以及它们的实现原理。最后提供了获取源码的链接。

还要总结其他网页吗? y/n
>

```
