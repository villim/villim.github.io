
---
title: Alfred Workflow Rename Ebook
layout: post
---

有个不好的坏习惯，有收集电子书的癖好 ... 看到喜欢的，感兴趣的，感觉自己会想看一看的，就想要收集起来。存了 13G 多的书，事实是大部分都没读，虽然个别可能会在10年后被突然翻出来看一下，然后感慨一下夫子远见 ... 无论如何，这癖好，暂时时改不了的了 :)

收集电子书，最大的问题，当然就是归类，这「学问」可就深了。当然，现在有了 Spotlight 或者 Alfred 这样的工具，可以非常快捷检索电脑上的文件，分类即使不够好，也不是大问题了。不过，查找是否效率，就取决于你能否给文件取个好名字了。我个人的喜好是以下面的方式命名：

**用 [] 分割信息，方便直观看，也方便设置分隔符；用 . 取代空格，避免命令行时尴尬。** 比如：

```
[Modern.Java.Recipes][Simple.Solutions.to.Difficult.Problems.in.Java.8.and.9][9781491973172][2017][EN].pdf
```

可要这么弄，手工一个一个敲起来，就不够愉快了。几个文件时还凑合，再多一点时，还真是要吐血的。当然，其实也一直都这么挺过来了... 一直想着，是不是应该自动化一下了，但拖了又拖。周六晚上，突然搜到《Learn AppleScript》这本电子书，突然想起 Mac 上还有这个玩意儿，简单看了一下，正是适合干这件事。配合 Alfred Workflow，很完美。

![Rename Ebook Alfred Workflow](http://villim.github.io/img/2020/rename-ebook-workflow.png)

花了一天时间来学了学 AppleScript，真心喜欢不起来 ... 故意要把语言变得「很自然」似的，却反而相当不利于编程时有结构性的理解。就像是学第三外语，明明知道干干嘛，可就是语法老是犯错误。Apple Script 本来做的事情并不复杂，也是「胶水」程序，可也不可能让普通零基础用户使用，真不明白干嘛要这么设计。不过现在已经直接支持 JavaScript 了，应该是明白以前太理想主义了。

因此，写起来真不是有趣的事情，最后拼凑了个能用的东西

![Rename Ebook with Alfred](http://villim.github.io/img/2020/rename-ebook-demo.png)


P.S.

1. Source and Alread workflow can be download from [Github](https://github.com/villim/alfred-workflow-rename-ebook)
2. Another Alfred Workflow for [Unit Convertor](http://villim.github.io/alfred3-workflow-unitconvertor) 
