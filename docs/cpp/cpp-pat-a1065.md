---
layout: post
title: [C++]——PAT-A1065 & cin与scanf
date: 2021-02-02
tags: ["C++","Study"]
---

# 题解代码链接

[A1065 A+B and C(64bit)](https://www.lip0041.top/2021/02/pat-1065-ab-and-c-64bit/ "PAT-A1065 A+B and C(64bit)")

* * *

# 题目说明

此题是考察溢出的问题，本应该是较为容易的题。但是由于我现在是在学习c++中，干啥都用`cin`/`cout`。
发现提交这个题的时候，第三个测试点用`cin`过不去，用`scanf`就过去了。于是就想着探究一番

# cin 与 scanf 探究

通过[查阅资料](https://blog.csdn.net/zoukangdlut/article/details/68941160?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-4.control&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-4.control "查阅资料")得知，`cin`是有4个条件状态量的：

    goodbit:无错误
    eofbit:已到达文件尾
    failbit:非致命的输入/输出错误，可挽回
    badbit:致命的输入/输出错误,无法挽回

而像这种输入格式不符合流设置的格式则出错，如`cin`一个`int`数据，但是其值为$2^{31}$=2147483648，产生上溢。

*   `cin`的处理

    此时`failbit`将被设置为1，表示出错，且此时`cin`输入的数据以全1表示出错，此处即为$2^{31}-1$=2147483647。</p>
*   `scanf`的处理

    此时输入的值为$-2^{31}$，即-2147483648

<p>`cin`返回false则出错，可以检测出这种failbit出错，即用`cin.fail()`。若`failbit`被设置了，则返回`true`。捕获到错误后，则可以通过`cin.clear()`清除状态标志位，即可以挽回。此时可继续输入新的值存入刚才要存入的变量中，之前的错误输入则被丢弃（这一点我其实有在查找能否不丢弃，重新利用，但没有找到这方面但资料🙃）
**若不清除状态标志位，则后续不能继续进行输入**
还有一个问题是，使用`int`是可以测出这个差别的，但此题是用`long long`型的，或许是因为目前机器（包括oj）基本都是64位的，所以在这里对`long long`的溢出处理`cin`和`scanf`是一样的。

**测试如图**
![输入数据](Screen-Shot-2021-02-02-at-23.21.39.png)
![结果](Screen-Shot-2021-02-02-at-23.22.20.png)

显而易见，`cin`与`scanf`的差异之处

对了，对于效率这方面，`cin`若使用了`cin.sync_with_stdio(false)`关闭同步，即可跟`scanf`效率差不多。
