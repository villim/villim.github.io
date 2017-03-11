---
title: 无法取消的开机启动APPS
layout: blog
---

## 幽灵启动项

重新启动Mac的时候，总是有几个APP，比如：百度云，Evernote，Box，Python IDE ... 一股脑地打开。真是无比恼人。

当然我并没有绝对的懒癌，还是花了好些时间琢磨过。OSX的话，开机启动设置不就是Login Items么？不过，断断续续遇到这个问题时，尝试取消了好几次都不起作用，仿佛幽灵，让我怀疑是不是GUI的Bug。后来想直到命令行里处理，不过最后还是懒在了这一步。毕竟，Mac几乎没有重启的时候，平时都是直接扣上屏幕了事的。

不幸的是，好日子到头了。最近被迫要关注一个lagacy project，项目太老代码太复杂就不吐槽了。不给Eclipse分配至少2G，根本就跑不起来，还动不动跑着跑着就死机了！WTF！每天要重启几次，便要手动关一大堆随机启动的Apps，真心痛苦了 -_-||

##  Unchck还是Delete？

和Johnson做事时顺便问了一下这个开机启动的问题。他说以前也是老是关不了，后来不知怎么，有次删掉重起就行了。好吧，显然他只是模糊的印象，没有实质的建议。不过提到这个“删除”，还是让我有看到火花的感觉。

为什么我之前在Login Items里面，是Uncheck而不是删掉呢？重新把 Login Items调出来看了一下，眼睛都要掉下来 (ｰ ｰ;) 

![OSX Login Items](http://villim.github.io/img/2017/login-items-settings.png)

**在LoginItems里面，打勾☑️的意思是 Hide(隐藏),而我一直以为是 Avtive(有效)!!** 最可气下面，那句说明，“To hide an applicaiton when you login, select the checkbox in the Hide coloumn next to the applicaiton.” 我是有切切实实读过好几遍的，却从来没有幡然醒悟过。

于是马上尝试直接删掉 ... 世界立刻就清净了。

##  经验主义的误区

害死你的往往不是你陌生的，而是你熟悉的东西。

淹死的都是游泳还不错的，水性不好的大多预案充分。[之前聊到Quanlity的时候也提到过，价值的陷阱](http://villim.github.io/review-of-zmm)： 比如你发现出了问题，可怎么都找不到原因。因为你的价值僵化了，总是固守以前的价值观，无法从新的角度看问题。

道理总是那么简单，想记住也不花时间，可找死却仍然是那么容易。毫无疑问，我又傻X了一次。啊啊啊啊啊啊啊啊啊啊 ～ 打脸啊打脸

![打脸啊打脸](http://farm3.static.flickr.com/2713/4518743336_4ac445bd9d_o.gif)




