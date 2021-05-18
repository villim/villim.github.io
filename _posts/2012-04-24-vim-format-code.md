---
layout: post
title: 用Vim开发 ： 格式化代码
categories:
- LINUX
- OTHER
tags:
- Vim
status: publish
type: post
published: true
meta:
  _edit_last: '1'
author:
  login: villim
  email: villim@126.com
  display_name: Villim
  first_name: Villim
  last_name: Wong
---

用 Vim 开发，第一个问题就是：如何格式化代码？之前关于 [Vim 配置](http://villim.github.io/vim-configuration-for-c)里已经有关于 Tab 的控制和配置自动缩进。

可是当然免不了要自己动手的时候.本来以为还需要安装插件才能把这事儿给办了，不过其实做起来相当方便快捷。

## 全文格式化

```bash
gg=G
```

## 格式化选择区

选择指定的一些代码来格式化: 

```bash
v [jk] =
```

也可以简单地格式化当前行:

```bash
==
```

## 格式化代码块

代码行里的  “{” 和 “}” 也能让我们快捷格式化：

```bash
=}        # format until }
={	       # format from {
```

要特别注意的是，当你的代码在{}里有多个代码块的时候，却并不能这样格式化所有的内容，比如有下面的代码：

``` java
protected Session getImapSession() {
        Properties props = new Properties(); // block 1
        props.put("mail.imaps.host", getHostname());

        return Session.getInstance(props); // block 2
    }
``` 

因为空行的关系，这个方法有2个代码块，这个时候 **=}** 或者 **={** 都不能格式化所有的东西。这个时候你需要指定**格式化代码块**：

```bash
=i}   //从当前行格式化到}
=i{   //从当前行格式化到{
```

### 格式化 Json 

为了让 Json 格式的数据便于显示，可以 简单的使用下面的命令:

```bash
:%!python -m json.tool
```
如果还想更简化操作，可以在 ~/.vim/vimrc 文件里定义一个快捷键:

```
nmap <F4> :%!python -m json.tool
```