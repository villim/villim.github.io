---
title: Byte Order Mark
layout: post
---

# 幺蛾子

处理一个客户提交的文件，类似这样的数据

```bash
﻿61121|A|BE060U5R|B|2016|DRAW_OTC|_NULL_|_NULL_|_NULL_
|465|465|N|N|N|N|N|N|N|N|N|2016-3-24T00:00:00|PHILLIPSE
```
把它转化为Object总是出错，看了看数组:

```bash
[﻿, 6, 1, 1, 2, 1, |, A, |, B, E, 0, 6, 0, U, 5, R, |, B, |, 2, 0, 1, 6, |, D, R, A, W, _, O, T, C, |, _, N, U, L, L, _, |, _, N, U, L, L, _, |, _, N, U, L, L, _, |, 4, 6, 5, |, 4, 6, 5, |, N, |, N, |, N, |, N, |, N, |, N, |, N, |, N, |, N, |, 2, 0, 1, 6, -, 3, -, 2, 4, T, 0, 0, :, 0, 0, :, 0, 0, |, P, H, I, L, L, I, P, S, E]
```
看起来也是挺正常的，不过 debug 看起来，我读出的字符，和看到的一定不一样。


# Invisible Characters

既然隐身了，用Vim来看看。如果你用的是GUI版本，比如MacVim，可以在Tools里面找到**Conver to HEX**. 如果在Terminal里面也很简单，运行这个命令：

```bash
:%!xdd      // convert to hex
:%!xdd -r   // convert back from hex
```

看不得人的家伙出现了：
 ```bash
0000000: efbb bf36 3131 3231 7c41 7c42 4530 3630  ...61121|A|BE060
0000010: 5535 527c 427c 3230 3136 7c44 5241 575f  U5R|B|2016|DRAW_
0000020: 4f54 437c 5f4e 554c 4c5f 7c5f 4e55 4c4c  OTC|_NULL_|_NULL
0000030: 5f7c 5f4e 554c 4c5f 7c34 3635 7c34 3635  _|_NULL_|465|465
0000040: 7c4e 7c4e 7c4e 7c4e 7c4e 7c4e 7c4e 7c4e  |N|N|N|N|N|N|N|N
0000050: 7c4e 7c32 3031 362d 332d 3234 5430 303a  |N|2016-3-24T00:
0000060: 3030 3a30 307c 5048 494c 4c49 5053 450d  00:00|PHILLIPSE.
0000070: 0a                                       .
``` 
显然 **36 3131 3231** 是 **61121**，那么这个 **efbb bf**是什么鬼？ 联想到客户是用的 Windows，想到这个东西：

| Byte order mark |  Description   | 
| :--------------------  | :------------- |
| EF BB BF |	UTF-8 |
| FF FE	| UTF-16, little endian |
| FE FF	| UTF-16, big endian |
| FF FE 00 00	| UTF-32, little endian |
| 00 00 FE FF	| UTF-32, big-endian |



# What is BOM

为什么有 BOM ，是一个很有趣的问题，[Character Encoding](https://en.wikipedia.org/wiki/Character_encoding) 也是一个很复杂很有深度的话题 (加入字体相关知识，就更丰富了).

更多的看[WIKI](https://en.wikipedia.org/wiki/Byte_order_mark)，简单来说就是：

Always prefix a Unicode plain text file with a byte order mark, which informs an application receiving the file that the file is byte-ordered. Available byte order marks are listed in the following table. Because Unicode plain text is a sequence of 16-bit code values, it is sensitive to the byte ordering used when the text is written.

因为UTF-8的Byte Order即使不写也是容易判断的，在Linux／Unix中，常常都是省略的。不过Windows的大多数编辑软件都是默认需要的。

# Remove BOM

现在问题简单了，可以在程序里支持，或者去掉BOM就好。还是说 Vim 的方法。

```bash
:setlocal nobomb   // remove BOM characters
:w 
```
```bash
:setlocal bomb?   // check if contains BOM
```

