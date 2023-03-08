+++
author = "瑞东"
title = "ChatGPT小工具(用Chat GPT 编程?)"
date = "2023-03-08"
description = "chatGPT"
tags = [
    "周末项目数据","博客"
]
categories = [
    "blog",
]

+++

最近写了2个Chat GPT的小玩具，有网页版，也有浏览器插件，源码和效果在首页有链接，总体来说开发这种小工具还是很简单的，官方提供了api使用文档，只需要copy过来做一个简单的用户界面即可，现在网上有很多套壳版，最开始使用体验还不错,不过现在大多数情况下都在用自己开发的浏览器插件 在浏览器任意位置 ctrl+shirt+x就可以欢迎对话。

**用Chat GPT 编程***

对了，现在写代码开始让Chat GPT 给输出一个基本的大纲，然后在进行修改和调整，lisp4js这个项目的parse模块就用到了GPT编写代码大纲，然后手动编写了对字符串类型和symbol类型的支持，这大大提高了编码效率；evaluate模块最开始是用Chat GPT生成的，但对于自定义函数的支持并不友好，及没有作用域，于是全部删除开始手动编码和调试，然后今天完成了初版，以前是面向谷歌编程以后要学习面向Chat GPT编程了及学习更多的prompt，编码的入门门槛也在此降低了许多，用人类语言告诉Chat GPT 然后他告诉你对应的代码，然后再做微调即可，我们需要做的就是学会和其更高效的对话。

这是一个示例

user：

> 用js写一个lisp的parser

ChatGPT:

>  由于LISP的语法比较复杂，写一个完整的解析器需要大量的代码量，因此这里只提供一个简单的LISP格式解析器的实现示例，仅用于学习和参考。

>  以下是一个简单的LISP解析器的实现，它包括了LISP的元素类型、符号表达式、数字表达式、列表表达式等：
```
function parseLisp(input) {
  input = input.trim();
  if (input[0] === "(") {
    let list = [];
    input = input.substring(1, input.length - 1).trim();
    while (input.length > 0) {
      let elem = parseLisp(input);
      list.push(elem.expr);
      input = elem.rest.trim();
    }
    return {"expr":list, "rest":""};
  } else if (input[0] === "\"") {
    let end = input.indexOf("\"", 1);
    let str = input.substring(1, end);
    return {"expr":str, "rest":input.substring(end + 1)};
  } else {
    let end = input.search(/\s/);
    if (end === -1) {
      end = input.length;
    }
    let sym = input.substring(0, end);
    if (isNumber(sym)) {
      return {"expr":Number(sym), "rest":input.substring(end)};
    } else {
      return {"expr":sym, "rest":input.substring(end)};
    }
  }
}

function isNumber(str) {
  return /^\d+$/.test(str);
}
```
>  这个解析器基本上是一个递归的函数，它把输入的LISP表达式逐渐转换成对应的JavaScript对象。该函数接受一个字符串作为输入，然后根据字符串的首字符来确定该字符串表示的是哪种类型的LISP表达式。如果LISP表达式是一个符号，该函数将其解析为一个字符串；如果是一个数字，该函数将其解析为一个数字；如果是一个列表，该函数将其转换成一个JavaScript数组，并递归处理列表中的每一个元素。

