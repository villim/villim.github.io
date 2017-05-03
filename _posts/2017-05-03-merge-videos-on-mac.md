---
title: 在Mac上合并视频文件
layout: post
---

在Youku上下载了几个驾考视频，结果被分成了很多小段。实在太不方便，于是想把它们合并成一个文件。花钱的解决方案挺多，不过不要钱的方法真花了点时间。

## Download Videos

顺带提一下，下载使用 [youtube-dl](https://rg3.github.io/youtube-dl/) 真是相当方便，看它名字就知道是给Youtube准备的，不过[很多视频网站](https://rg3.github.io/youtube-dl/supportedsites.html)都是支持的。除了Mac版本，Windows也是支持的，使用非常方便：

```bash 
## install youtube-dl
$ brew install youtube-dl

## List all available formats of requested videos
$ youtube-dl -F [videos_url]

## download with mp4
$ youtube-dl -f h5 [videos_url]
```

## Convert Videos

如果需要格式转换，可以考虑使用免费的 [HandBrake](https://handbrake.fr/)。几乎支持所有格式。使用也不是很复杂，不过还是需要花点时间研究。毕竟视频文件里面的花花肠子不少。

![HandBrake](https://handbrake.fr/img/slides/slide2_mac.png)

## Merge videos

找这个很麻烦，不用花钱的选择并不多。最后解决问题的是 **QuickTime Player** !! 没有这茬，根本想不起来还有它了。我目前的的版本是 10.4

1. Open 1st video part
2. Edit -> Add Clip to End -> 2nd video part
3. Edit -> Insert Clip After Selection -> 3rd video part
4. ( ... repeat aciton 3 )
5. File -> Export 

使用Quicktime的问题是，仅支持Mp4。如果要想支持更多格式，可以安装 [Perian](http://perian.org/)，不过对我来说mp4已经足够好了。
