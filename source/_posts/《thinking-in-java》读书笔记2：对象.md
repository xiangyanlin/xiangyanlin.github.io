---
title: 《thinking in java》读书笔记2：对象
date: 2019-12-04 21:05:30
categories:
  - 读书笔记
    - thinKing in java
tags: 笔记
---

BigInteger:支持任意精度的整数
BigDecimal:支持任何精度的定点数
java的作用域由{ }决定，

<!--more-->

#### java基本成员变量默认值
boolean:false, char：'\u0000'(null), byte:0, short: 0, int：0，long: 0L, float: 0.0f, double:0.0d
#### javadoc
javadoc 命令只能出现在"/**"注释中出现，主要有两种方式。
1，文档标签,
（1）独立文档标签：以"@"开头
 （2）行内文档标签：同样以"@"开头，但是要括在"{}"内。
2，嵌入html
如: 

```
/**
*<ol>
*<li>item one
*</ol>
*/
```