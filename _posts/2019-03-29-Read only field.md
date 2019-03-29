---
layout:     post
title:      只读字段
subtitle:   readonly
date:       2019-03-29
author:     zx
header-img: img/post-bg-miui6.jpg
catalog: true
tags:
    - .NET
    - C#
---

## C#只读字段
### readonly

常量的概念就是一个包含不能修改的值的变量，但是，常量不必满足所有的需求，有时候需要一些变量，其值不应改变，但在运行之前其值是未知的。  
**readonly**关键字比const灵活的多，允许把一个字段设置为常量，但还需要执行一些计算，以确定它的初始化值。  
其规则是可以在构造函数中给只读字段赋值，但不能再其他地方赋值。  
只读字段还可以是一个实例字段，而不是静态字段，类的每个实例可以有不同的值。  
