---
layout: post
title: Ubuntu 11.10 Solution Problem
categories:
- LINUX
tags:
- Solution
- Ubuntu
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
<p>这周把公司的物理工作区换了换位置，不知怎么回事竟然影响到了 Ubuntu 那台开发机的分辨率，好好的1280x1024却被弄得只有1024x768，而且配置里根本没有 1024 以上的选项，怎么也改不回来。现在回想起来，刚搬回来的时候，错误的把显示器插在了主板的VGA口上，而不是显卡的VGA口，但是!! 如果这就是元凶的话，也真够 Stupid 的 !!</p>
<p>好了，郁闷没有用需，还是要解决问题。首先怀疑是驱动问题，因为 Nvidia 的显卡，出问题也是挺正常的，Windows 下都弱爆了，更不要说 Linux。先到 “ <strong>Additional Drivers</strong> ” 里查看一下，显卡驱动正常。然后想查看 /etc/X11/xorg.conf ， 可是竟然没有，没弄懂 Ubuntu 把东西写道哪儿去了。但是可以通过下面的命令来实现配置。</p>
<p><span style="color: #993300;"><strong>查看当前的分辨率设置：</strong></span></p>
<pre class="brush:shell">villimw@Skynet:~$ xrandr -q
Screen 0: minimum 320 x 200, current 1024 x 768, maximum 8192 x 8192
VGA1 connected 1024x768+0+0 (normal left inverted right x axis y axis) 0mm x 0mm
   1024x768       60.0* 
   800x600        60.3     56.2  
   848x480        60.0  
   640x480        59.9</pre>
<p><span style="color: #993300;"><strong><strong><strong>方式1：</strong></strong>计算 1280x1024 参数：</strong></span></p>
<pre class="brush:shell">villimw@Skynet:~$ cvt 1280 1024
# 1280x1024 59.89 Hz (CVT 1.31M4) hsync: 63.67 kHz; pclk: 109.00 MHz
Modeline "1280x1024_60.00"  109.00  1280 1368 1496 1712  1024 1027 1034 1063 -hsync +vsync</pre>
<p><span style="color: #993300;"><strong><strong><strong>方式1：</strong></strong>添加并配置为 1280x1024 分辨率：</strong></span></p>
<pre class="brush:shell">villimw@Skynet:~$ xrandr --newmode "1280x1024_60.00"  109.00  1280 1368 1496 1712  1024 1027 1034 1063 -hsync +vsync
villimw@Skynet:~$ xrandr --addmode VGA1 1280x1024_60.00
villimw@Skynet:~$ xrandr --output VGA1 --mode 1280x1024_60.00</pre>
<p><span style="color: #993300;"><strong><strong>方式1：</strong>你可能要启动时自动重新配置分辨率：</strong></span></p>
<p>奇迹诞生了！ ^_^ 1280 出现了，但是在我的机器上，并不是满屏~ 我天真的以为这是因为大概要重启吧。如是重启之，结果让人失望的是竟然回到了 1024x768。好吧，在 ~/.xprofile 把上面的命令写进去：</p>
<pre class="brush:shell">villimw@Skynet:~$ xrandr --newmode "1280x1024_60.00"  109.00  1280 1368 1496 1712  1024 1027 1034 1063 -hsync +vsync
villimw@Skynet:~$ xrandr --addmode VGA1 1280x1024_60.00
villimw@Skynet:~$ xrandr --output VGA1 --mode 1280x1024_60.00</pre>
<p>再重启，1280x1024 出现了，但是！依旧不是满屏的 -_-||  继续寻找解决这个问题的方法，我重装了显卡驱动，甚至是 X Server ... 于是当然，更大的悲剧出现了，系统彻底毁掉了 ~~ 彻底的 ~~~ 剩下的解决方案竟然只剩下了 “<span style="color: #008000;"><strong>重装</strong></span>”。</p>
<p>当然重装也不是坏事 Ubuntu 11.10 有颇让人满意的地方，可是总让人有些 “不放心” 的感觉，而且 <strong>Unity </strong>界面虽然也不错。可把所有特性都给毁了，显卡等于白占地儿，不XXXX 。这倒是一个不能选择的机会让我回到 10.10，而且那个版本更“稳定”，使用 gnome ，估计不会向 Unity 一样经常卡死 ...</p>
<p>可是真的更稳定吗？令人“大吃一斤”的居然 10.10 装好了还是只有 1024x768 !! NNDX ~  然后又是一轮驱动配置 ... 最后还是要看 <strong>xorg.conf</strong>，霸王的解决方法。</p>
<p><span style="color: #993300;"><strong>方式2： 修改 ~/X11/xorg.conf</strong></span></p>
<p>你可以自己新建这个文件。不过我建议是：在调用 “System -&gt; Preferences -&gt; Monitors” 的时候，会提示 “ Do you want to use your graphics driver vendor's tool instead?” ，选择 Nvidia 提供的工具，选择 “X Server Display Configuration” ，然后点击按钮 “Save to X Configuration File”。然后手工作如下内容 ：</p>
<pre class="brush:plain">Section "Monitor"

 # HorizSync source: builtin, VertRefresh source: builtin
 #28.0 - 55.0
 #43.0 - 72.0
    Identifier     "Monitor0"
    VendorName     "Unknown"
    ModelName      "CRT-1"
    HorizSync       31.0 - 81.0   ---》  修改此处
    VertRefresh     56.0 - 76.0  ----》  修改此处
    Option         "DPMS"
EndSection</pre>
<p>好了，重启，世界回复和平了！~ 回想起来 Ubuntu 11.10 的时候，其实这么干也一定能成功。不过已经回到 10.10 了，还是继续使用飘逸的 3D 动态效果吧 ^_^</p>
