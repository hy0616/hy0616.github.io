---
title: 使用select2插件遇到问题总结
date: 2017-01-08 17:51:23
tags: [javaScript,select2]
categories: javaScript
---

**官方文档地址[链接](http://select2.github.io/)。**

#### 报错解决

<!--more-->

**错误1:** 当使用本地或远程数据时可能会报`Uncaught Error: Option 'ajax' is not allowed for Select2 when attached to a <select> element`类似错误。

**解决办法:** 将select标签换成div标签，显示正常。

**错误2：** 如果select2插件引用时，展示框出现样式问题。

**解决办法:** 可查看li标签样式，或设置select宽度。
