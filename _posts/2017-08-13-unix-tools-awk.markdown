---
layout: post
title: "实用UNIX工具AWK"
author: "Wang"
date: 2017-08-13 21:34:12
header-img: img/post-bg-2015.jpg
tags:
  - UNIX
  - Tools
---

## 什么是AWK
首先，AWK的名称来源于三个作者名称的首字母，名称本身没有什么特别的含义。AWK是一个结构化文本处理工具，经常用来从结构化文本数据中统计数据生成报表，或者统计一些数据得出结果并输出到标准输出，当然其本身强大的功能并不仅限于此。

## AWK如何工作
### 记录和域
简短来说AWK首先要从一个文本中读取记录，然后拆分域，在尝试对记录进行匹配（pattern），如果匹配成功则执行相应的动作（Action）。  
AWK在缺省状态下用换行来分割记录，用空格来分割域
。假设下面是一个文件内容，

>Lucy 120  20  
>Jack 130  21  

当AWK处理此文件的时候，在参数缺省状态下，会将Lucy 120 20当成一条记录，Jack 130 21当成一条记录，Lucy这条记录将分成三个域分别是Lucy 120 20，Jack也是如此划分。以下命令将打印每条记录的第二个域，我们可以在awk程序中使用“$N”的形式表示域的内容，$0表示整条记录。

    awk '{print $2}' inputfile.txt
    // 将输出以下内容
    120
    130


## pattern与action  

在上面的例子中,pattern是缺省的，action就是“{print $2}”,当pattern缺省状态下，默认是匹配每个记录。同样action也可以省略，缺省状态下的action则是{print $0}，语义是输出整条记录。pattern和action只能缺省其中一个而不能两个都缺省。首先我们先看几种常见的pattern形式。  

* 正则匹配pattern
* begin／end
* beginfile／endfile
* 表达式pattern

#### 正则匹配pattern



