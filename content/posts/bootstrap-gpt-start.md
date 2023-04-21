+++
author = "瑞东"
title = "Bootstrap GPT 如何使用"
date = "2023-04-21"
description = "ChatGPT 如何使用及一些例子"
tags = [
   "博客","GPT"
]
categories = [
    "blog",
]

+++

## 第一步：

访问 https://github.com/weekend-project-space/bootstrap-gp 点击 code download zip 按钮 或通过命令行下载

```
> git clone https://github.com/weekend-project-space/bootstrap-gpt.git
```

## 第二步：

进入项目文件夹 或命令行进入 , 安装依赖（ 请保证本地有 python3 的运行环境）, 配置自己的 api-key

```
> cd ./bootstrap-gpt


> pip install openai && pip install beautifulsoup4 && pip install jsonpath && pip install jinja2
```

在.env 文件修改 api-key

```
api_key=sk-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

## 第三步：

运行项目

```
> python3 main.py
```

此时命令行会输出

```
Welcome to Bootstrap GPT
sample > use summarize
>
```

然后可以输入 help 了解有那些命令，常用命令有三个

- ls: 查看有那些功能
- use xxx: 使用 xxx 功能
- serve: 开启 http server 功能可以网页访问

---

## 进阶

正常情况下到这里就可以了，如果想要更多功能可以在 bootstrap 文件夹下创建 json 文件，一个功能文件如下

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

这是一个总结网页的功能
我们重点关注 boot 这个字段， boot 是一个数组，数组里面有多个对象，对象有如下几个字段

- w: write 支持模板变量 向用户界面输出内容
- r: read 读取用户的输入信息存放在后面的 r0 字段中
- b: branch 分支 支持 Object 类型字段 eq 跳转 和 Array 循序执行 或 无继续往下执行， -1 为结束执行 如第三个对象中的 y:0 ,n:-1 ,当输入为 n 时结束执行
- p: prompt 支持模板变量 微指令 用于引导 chatgpt[chat:] 给其文案 或 爬虫[sprider:]搜索 纯文本[text:]输出， 可以扩展更多微指令提示引导 如 +: -: len: ，必须微指令开头后面写模板内容

r0 m1 r2 为变量名称 为类型+index 索引 有 r：reader w:writer p:prompts m:msg 之分

r0 r2 是我们自己定义的读入信息存放的字段， m1 是下标为 1 的对象 p 处理后的返回信息

## 扩展

- [bootstrap-gpt](/posts/bootstrap-gpt): 了解命令是如何运行的
