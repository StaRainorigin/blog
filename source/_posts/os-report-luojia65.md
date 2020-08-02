---
title: 洛佳：操作系统实验总结
date: 2020-07-15 14:34:11
categories:
	- report
tags:
	- author:luojia65
	- summerofcode2020
	- rcore-lab
mathjax: true
---
我是洛佳，参与了这次OS实验。我在一段时间的工作中，学习了大量操作系统开发的基础知识，熟悉了理论课的概念。
RISC-V是崭新的架构，Rust是优秀的编程语言，都是全新的技术和工业设计的精华。这样开发操作系统，学习的效果更好。
本次实验我还尝试为开源社区提出意见，帮助建设Rust与操作系统相关的生态环境。
<!-- more -->

这次的实验有两个部分，学习Rust、RISC-V指令集，以及开发自己的操作系统。

## Rust语言与程序设计

Rust是一门优秀的语言。我们不谈保守或激进的宣传词，不叙述大量公司的开发实践，只从愿意“吃螃蟹”的人们谈起，
就能对Rust独特的设计略窥一二。

学习Rust语言一开始遇到的问题不会少，通常遇到的坎会有几个。一个是生命周期，一开始遇到通常是发现`&str`
偶尔会提示缺参数。还有就是裸指针和不安全代码，要认识到Rust的目的是管理不安全，而不是消灭不安全。
裸指针在编写数据结构上用途是非常广的。最后有一点就是相关的接口设计，比如切片（Slice）里面是有元素交换函数的，
很多初学者第一个想法是用`mem::swap`然后想办法拿出两个可变借用，这其实是做不到的，应该用已有的函数。

有一些Rust的特性，其它语言的开发者也不容易想到。比如Rust拥有一系列零长度类型，以单元类型“`()`”做例子，
对它做任何的运算操作，最终都将编译到空指令。它在内存中占用零个长度，取值只有一种可能性，所以它的读写操作
也不需要经过内存，只需要填写唯一的可能性就可以了。利用这些零长度类型，能做出很多独特的设计。
此外，Rust默认的所有权语义也能很好地描述硬件，可以避免一些情况的数据冲突问题。

Rust语言的生态非常好，至少目前的工作已经能符合实验需求。学Rust语言是循序渐进的过程，张老师的话很对，
要从整体上把握这是一门怎样的技术。

## 第五代精简指令集技术

我希望给RISC-V这样一个中文名，有点像一些科普作者给5G技术取的中文名一样。
不过不管怎样称呼，它是吸收了大量指令集的先进之处。我虽然对处理器设计只是入了门，只这样浅薄地给一些自己的看法。
从实践来说，是一个设计非常前卫的指令集技术，已经有逐步在市场推广的苗头。
未来很可能仍然有更先进的技术，但RISC-V的包容性是极强的。希望它能持续在市场活跃至少五十年。

## 操作系统不简单

这次实验要写的操作系统，很多部分都是斟酌之后的工程设计。或者说，其实那样写是可以的，为什么这样写呢，
这样写的优点比别的写法要多。还有很多可以做得不同的设计，比如设备树的具体实现等等，
在算法之外的部分，就是操作系统要暴露给用户的规范了。接口设计方法的不同，操作系统的风格就不同，这也是
开发操作系统的魅力所在。

我们目前还只在编写简单的操作系统内核。后面假如要继续完善生态圈，兼容各种各样的硬件都是需要的，
运行在用户层上的操作系统工具也是需要的。我们应当能解析各种各样的硬件，做出统一的抽象，这才是操作系统开发
的重要一步。有了这些事项，就可以考虑如何做得让用户喜欢了。

可以用Rust和RISC-V写操作系统，这是非常划算的想法。即使我们的操作系统可能也兼容到别的指令集，
学习新的架构和知识仍然是比较赚的。等我们先投资时间成本，我们就能多学一点。

## 一些感想

这一个月在实验室的学习，反过来让我回顾操作系统的基本知识。虽然我并未在学校上过这样的课，
我还是看了很多网课，有时候实践之后再回来看理论，是真的会有不一样的想法。
我这个月给社区提了非常多的意见，很多都被采纳了，我还去参加了很多活动，这是我非常高兴的一点。希望未来的开发经历里，我能学到更多的知识。
这样的教程能出现，我感觉非常赞同，希望我们一起学习的朋友们能做成社区的成员，未来为开源多尽一份力。