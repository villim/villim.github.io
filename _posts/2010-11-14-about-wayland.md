---
layout: post
title: 关于 Wayland
categories:
- LINUX
tags:
- Ubuntu
status: publish
type: post
published: true
meta: {}
author:
  login: villim
  email: villim@126.com
  display_name: Villim
  first_name: Villim
  last_name: Wong
---
<p>除了Ubuntu外，看到 Federo 也开始申明说将支持 <span style="font-family: Georgia, 'Bitstream Charter', serif; color: #333333;"><a href="http://wowubuntu.com/unity-on-wayland.html">Wayland X-Server</a>。</span></p>
<p>不能不对这个据说能够深刻震撼 Linux 图形界面，可能改变Linux 未来的东东有了点兴趣。</p>
<p>本来想写点什么，不过网上已经有了很好的文章介绍 (发现他家网站文章可能会访问不到，转一下)：</p>
<h3><span style="color: #008000;">Link : 1. <a href="http://www.ibentu.org/2010/11/06/introduce-to-wayland-01.html" target="_blank"><span style="color: #008000;">X Window的前生今世</span></a> </span></h3>
<p><a href="http://www.ibentu.org/tag/wayland">Wayland</a>是什么呢？它是X Window？还是要取代X Window？它的优势在哪里？Linux桌面/移动会因此有什么变化？在本篇中，我将回顾历史，展望未来，通过简易的文字，来先回顾一下X Window，从而继续解答Wayland。</p>
<p>注：在下对X Window的理解仅限于表面，文章中会有不少技术、历史方面的错误，若有大侠指出，不胜感激！</p>
<p><span style="color: #993300;"><strong>古老的X Window和现代的桌面技术</strong></span></p>
<p>X Window在1984年由MIT研发，它的设计哲学之一是：提供机制，而非策略。举个最简单的例子吧：X Window提供了生成窗口（Window）的方法，但它没规定窗口要怎么呈现（map）或摆放（place），这个策略是由外部程序——窗口管理器 （Window Manager）所决定的。另外一个X Window的主要特点便是：Server/Client网络模型。不论是本地、远程的应用程序，都统一通过Server/Client模型来运作，比 如：让远程的应用程序跑在本地上。</p>
<p>X Window在推出之后快速演化，在1987年时候，其核心协议已经是第11版本了，简称：x11。这个版本已经将“提供机制，而非策略”这个哲学贯彻地 非常彻底，以致于核心协议基本稳定，不需要特别大的改动。于是乎，你看到了，现在是2010年，整整23年了，X Window依然是X11。</p>
<p>你可能会诧异，23年了，X Window的核心都没有特别大的变化，它能适应现代桌面的快速发展吗？这就要再次提到X Window的设计优势了，X Window在核心层之外提供一个扩展层，开发者可以开发相应扩展，来实现自己的扩展协议，比方说：</p>
<blockquote><p>标准的Window都是矩形的，我如何用它来画一个圆形的窗口？X Window协议并未提供，但是通过“shape”这个扩展，X Window可以实现不规则的窗体</p></blockquote>
<p>所以啊，这23年，X Window除了继续完善核心协议、驱动以外，很大程度上，都是扩展使它保持“与时俱进”，比如说：</p>
<ul>
<li>要多头显示支持，这个是由“Xinerama”扩展实现的；</li>
<li>要有多媒体视频回放的支持，这个是由“X Video”扩展实现的;</li>
<li>OpenGL的3D支持，则是通过“GL”扩展来实现的；</li>
<li>Compiz那样的合成桌面特效是怎么弄的？没错，还需要一个新的扩展，它便是：“Composite”；</li>
<li>甚至Keyboard的支持，都是通过“X Keyboard Extension”（也就是“XKB”）的！</li>
</ul>
<p>X Window的核心，基本上就是在处理Server/Client、驱动之类的，而外部的那些支持，基本上全是通过“扩展”进行的。这没什么不好，X Window的结构设计精良，尽管是扩展，但它们没有任何效能上的问题。通过扩展方便地实现了一些对新技术、新事物的支持，而且方便维护，这再好不过了。</p>
<p>所以你看到了尽管23年过去了，基于X Window的GNOME、KDE，还能保持与同期Windows、Mac OS X竞争甚至某些方面更好，你就不得不佩服这些前辈在最初设计时定下的设计哲学是多么正确了。</p>
<p>虽然扩展的众多没有给X Window造成什么问题，也跟X Window的设计哲学相符，但是其Server/Client的网络构架，却一直倍受质疑，这便是：</p>
<p><span style="color: #993300;"><strong>X Window的效率问题</strong></span></p>
<p>经常听到有人说，X Window的Server/Client结构严重影响效率，导致Linux桌面的效应速度一直不如Windows、Mac OS X。事实是不是这样呢？让我们还是透过原理来说话吧。</p>
<p>这张，便是当前X Window系统的架构图，稍微解释一下：</p>
<ul>
<li>X Client：图形应用程序，如Firefox、Pidgin等；</li>
<li>X Server：你看不见的控制中心；</li>
<li>Compositor：合成桌面系统，如Compiz；</li>
<li>Kernel/KMS/evdev：这便是Linux Kernel，后面会提到<a href="http://imtx.me/tag/kms">KMS</a>技术了，其中还有一项evdev，是管理输入设备的。</li>
</ul>
<p><a href="http://imtx.me/static/uploads/2010/11/x-architecture.png"><img src="assets/x-architecture.png" alt="X Architecture" /></a></p>
<p>通过这些箭头，你已经可以明白一些X Window的工作机制了，不过还从一个应用场景来解释一下，想像一下，当你点击了Firefox（X Client）的“刷新”按钮，将会发生以下事情：</p>
<ol>
<li>你用鼠标点击了Firefox的“刷新”按钮，这时内核收到了鼠标发来的事件，并将其通过evdev输入驱动发送至了X Server。这时内核实际上做了很多事情，包括将不同品牌的鼠标发出的不同信号转换成了标准的“evdev”输入信息。</li>
<li>这时X Server可以判断哪个Window该收到这个消息，并将某座标按下按钮的消息发往X Client——Firefox。但事实上X Server并不知道它得到的窗口信息是不是正确！为什么呢？因为当前的Linux桌面早已经不是10年前的那样了，现在是“Composite”即合成 桌面的时代，合成桌面的一个特点便是：Compositor（如Compiz）管理窗口的一切，X Server只能知道屏幕的某个点收到了鼠标消息，却不知道这个点下面到底有没有窗口——谁知道Compiz是不是正在搞一个漂亮的、缓慢的动画，把窗口 收缩起来了呢？</li>
<li>假设应用场景没这么复杂，Firefox顺利地收到了消息，这时Firefox要决定该如何做：按钮要有按下的效果。于是Firefox再发送请求给X Server，说：“麻烦画一下按钮按下的效果。”</li>
<li>当X Server收到消息后，它就准备开始做具体的绘图工作了：首先它告诉显卡驱动，要画怎么样一个效果，然后它也计算了被改变的那块区域，同时告诉Compiz那块区域需要重新合成一下。</li>
<li>Compiz收到消息后，它将从缓冲里取得显卡渲染出的图形并重新合成至整个屏幕——当然，Compiz的“合成”动作，也属于“渲染（render）”，也是需要请求X Server，我要画这块，然后X Server回复：你可以画了。</li>
<li>整个过程可能已经明了了，请求和渲染的动作，从X Client-&gt;X Server，再从X Server-&gt;Compositor，而且是双向的，确实是比较耗时的，但是，事实还不是如此。介于X Window已有的机制，尽管Compiz已经掌管了全部最终桌面呈现的效果，但X Server在收到Compiz的“渲染”请求时，还会做一些“本职工作”，如：窗口的重叠判断、被覆盖窗口的剪载计算等等（不然它怎么知道鼠标按下的坐 标下，是Firefox的窗口呢）——这些都是无意义的重复工作，而且Compiz不会理会这些，Compiz依然会在自己的全屏幕“画布”上，画着自己 的动画效果……</li>
</ol>
<p>从这个过程，基本可以得出结论：</p>
<ol>
<li>X Client &lt;-&gt; X Server &lt;-&gt; Compositor，这三者请求渲染的过程，不是很高效；</li>
<li>X Server，Compositor，这两者做了很多不必要的重复工作和正文切换。</li>
</ol>
<p>当然，这里我没有直接说明这种模式有没有给X Window造成效率问题，因为我们还少一个对照组。再看对照组之前，再来看看X Server的另一个趋势：</p>
<p><span style="color: #993300;"><strong>从“什么都做”到“做得越来越少”的X Window</strong></span></p>
<p>X Window刚出现那会，主要提供一个在操作系统内核上的抽象层，来实现一个图形环境。所谓图形环境，最主要的便是：图形＋文字。当时的X Window便提供“绘图”和“渲染文字”的机制。图形桌面上的图案和文字，都通过X Window合成并绘制出来。</p>
<p>一个典型的例子，如果你要用X来画点，就要在你的程序中通过“XDrawPoint”来进行，X Server收到消息后，便会画出相应的点。</p>
<p>现在，稍微接触过图形开发的人都知道了，在X Window下，一般都通过GTK+和Qt来进行了。更深一层的是，通过Cairo（Qt不是）来绘制图形。Cairo是什么？它是一个绘图＋渲染引擎，著名的浏览器Firefox，便是使用Cairo来渲染网页和文字的。</p>
<p>Cairo是一个全能的、跨平台的矢量绘图库，它不是简单的包装一下各个平台的绘图库而已，尽管它最初是基于X Window开发出来的绘图库。现在Cairo支持各种不同的后端，来向其输出图形，比如X、Windows的GDI、Mac OS X的Quartz，还有各种文件格式：PNG、PDF，当然还有SVG。可以说，Cairo是一个很彻底的、全能的绘图库，现在无论绘制什么图形，都不会考虑到用XLib了。</p>
<p>在Cairo之上，还有文字排版库：Pango，同样很明显的，处理文字排版，都不会用XFont之类的东西了，而是直接用Pango画。当然Pango也是跨平台的。</p>
<p>尽管在Linux平台下，Cairo、Pango的发挥依然是基于X Window的，但X Window充其量仅仅是一个“backend”而已，并不是少它不行。同理，跨平台的GTK+、Ｑt也只是视X为其中所支持的后端之一，假如哪天X真的 不在了，更换一个新后端，当前的GNOME、KDE也能完整的跑起来。</p>
<p>再提另外一个比较典型的关于“X曾经做的，但现已不做”的例子，便是“模式设置（mode-setting）”，说通俗点，就是“分辨率的设置”，但后面会说明不仅仅如此。</p>
<p>大家都知道，Linux只是一个内核，它只有控制台，通过Shell来进行交互，而控制台默认是80×24（单位：字符）的，要进入分辨率1024×768或更高的图形模式，就需要X进行一次“模式设置”，设置正确的分辨率等等。</p>
<p>尽管后来Linux也支持了各种用户层（user-space）的模式设置，让终端也支持标准的分辨率，但是X的模式设置与此是不相干的，所以一两 年前，在Linux的启动过程中，从终端进入图形界面时，屏幕会“闪”一下，这时便在进行“模式设置”——这里就一定要用“模式设置”这个术语了，因为即 使终端是1024的，进入X图形也是1024的，模式的变更还是要进行。</p>
<p>后来呢，嗯，2009年初期，KMS（内核模式设置）终于出现了！！！很少关心桌面图形的Linux内核，在当时引入了“内核级”的模式设置，也就是说，在内核载入完毕、显示驱动初始化后很短的时间内，即设置好标准的分辨率和色深，通过在X层做相应的更改，从此X的初始化就可以省去“模式设置”这一 过程了！也就是从Fedora 10开始，Linux的启动非常平滑、漂亮，没有任何闪烁了。现在的Ubuntu 10.10也一样，KMS的应用已经相当成熟。</p>
<p>X从此又少了一样图形任务……“X泪奔～你们都不要我了。”</p>
<p>可以说，这20多年来，X从“什么都做”已经到了“做的越来越少”。绝大多数的开发者开发图形应用程序，已经可以完全无视X的存在了，X现在更像是一个中间人的角色。那么，X这个中间人会不会有一天，完全被其他事物所取代呢？</p>
<p>没错！它便是下篇要介绍的：Wayland！！！</p>
<h3><span style="color: #008000;">Link : 2. <a href="http://www.ibentu.org/2010/11/06/introduce-to-wayland-02.html" target="_blank"><span style="color: #008000;">Wayland应运而生</span></a></span></h3>
<p>&nbsp;</p>
<p>如果在两年前，按照那篇《<a href="http://www.ibentu.org/2010/11/2008/11/04/linux-new-x-server-waylan.html">Wayland：Linux的新X Server</a>》的理解，它是一个新的“X Server”，在于改善当前X Server的不足，从而取代它。现在，我们已经可以用更标准的语言来定义Wayland了，那就是：A Simple Display Server。</p>
<p>没错，Wayland是一个简单的“显示服务器”（Display Server），与X Window属于同一级的事物，而不是仅仅作为X Window下X Server的替代（注：X Window下分X Server和X Client）。也就是说，Wayland不仅仅是要完全取代X Window，而且它将颠覆Linux桌面上X Client/X Server的概念，以后将没有所谓的“X Client”了，而是“Wayland Client”。</p>
<p>更确切的说，Wayland只是一个协议（Protocol），就像X Window当前的协议——X11一样，它只定义了如何与内核通讯、如何与Client通讯，具体的策略，依然是交给开发者自己。所以Wayland依然是贯彻“提供机制，而非策略”的Unix程序。</p>
<p>“什么？Wayland还是Server/Client模式？”可以这么理解，但实际上与X Window的Server/Client有着本质的区别。</p>
<p>让我们用一张类似前文所示的图表来重新演示一下，在Wayland的框架下，窗口事件的响应是如何进行的。</p>
<p>在Wayland的架构图中，最显著的一些特点是：</p>
<ul>
<li>它复用了所有Linux内核的图形、输入输出技术：KMS、evdev，因此已支持的驱动可以直接拿来用；</li>
<li>Wayland没有传统的Server/Client的模式，取而代之的是：Compositor/Client，这不仅仅是换一个名称而已，后面会讲到具体区别；</li>
</ul>
<p><a href="http://imtx.me/static/uploads/2010/11/wayland-architecture.png"><img src="assets/wayland-architecture.png" alt="Wayland Architecture" /></a></p>
<p>还记得前文中“点击Firefox的刷新按钮”这个应用场景吧？在Wayland里，所有的流程是这样的：</p>
<ol>
<li>内核收到了鼠标发出的信息，经过处理后转发到了Wayland Compositor，就像之前发往X Server一样。</li>
<li>Compositor收到消息后，立马能知道哪个窗口该收到这个消息，因为它就是总控制中心，它掌握窗口的层级关系、动画效果，因此它知道该坐标产生的鼠标点击信息应该发送给谁，就这样，Compositor将鼠标的点击信息发送给了Firefox。</li>
<li>Firefox收到了消息，这时如果是在X Window下的话，Firefox会向X Server请求绘制按钮被按下的效果。然而在Wayland里，Firefox可以自行进行绘制而不需要再请求Compositor的许可！这就是传说 中的：直接渲染机制（Direct Render）！Wayland不管Client的绘制工作，整个过程变得十分简单而且高效！当Firefox自行完成了按钮状态的绘制后，它只需要通知 Compositor，某块区域已经被更新了。</li>
<li>Compositor收到Firefox发来的信息的，再重新合成那块更新的那块区域，将最终桌面效果呈现给用户。这个过程主要是跟内核、显卡驱动打交道了。</li>
</ol>
<p>整个流程是不是很自然、很简单？</p>
<p>所以结论出来了：</p>
<ol>
<li>Wayland的“直接渲染架构”彻底结束了传统X Window在渲染图形时需要不停的向Server请求、确认再绘制这个繁琐的过程，理论上响应速度有了“爆发式”增长；</li>
<li>Wayland从根本上消除了“Server+Compositor”的重复劳动，仅有且只需要有一个“Compositor”合成器而已。</li>
</ol>
<p>Compostior，就是Wayland上的“X Server”，但是它更纯粹，它不像X Server一样，像个大家长，什么都要管。Compositor只做该做的事情，把上面的过程简化成任务便是：</p>
<ol>
<li>基于Wayland协议，处理evdev的信息；</li>
<li>通知Client（即应用程序）对相关事件做出反应（至于应用程序想怎么反应，Compositor不需要过问）；</li>
<li>收到Client的状态更新，重新合成图形或管理新的图形布局。</li>
</ol>
<p>你意识到了，Wayland Compositor的角色，就像是“X Server”＋“Window Manager”，但它只做份内的事情而已。我想你已经可以想像Wayland构架是如何简单而且高效了，它一举解决了“X Window”发展这么多年来积累的、通过“扩展”去解决的那些问题。</p>
<p>看似很美好，那么Wayland现在的可用性如何？大家都知道，GTK+、Qt，现在都是基于X的，它们能顺利地移植至基于Wayland吗？当然可以！</p>
<p><span style="color: #993300;"><strong>逐渐成熟的Wayland周边应用</strong></span></p>
<p>还记得前面那篇文章中，我说过的这句话吧：“尽管在Linux平台下，Cairo、Pango的发挥依然是基于X Window的，但X Window充其量仅仅是一个“backend”而已，并不是少它不行。同理，跨平台的GTK+、Ｑt也只是视X为其中所支持的后端之一，假如哪天X真的 不在了，更换一个新后端，当前的GNOME、KDE也能完整的跑起来。”</p>
<p>你已经想到了，GTK＋、Qt，只需要简单的处理一下后端，便可以跑在Wayland上了。比如：</p>
<p>在当前的GTK+3.0开发分支中，有一个开发分支是“<a href="http://git.gnome.org/browse/gtk+/log/?h=rendering-cleanup">rendering-cleanup</a>”。“清理渲染”？这是做什么的？联想一下那个连Client“怎么渲染”都要管的X Server吧。</p>
<p>对了！GTK+3.0已经彻底移除了所有图形渲染、绘图方面跟X相关的部分了，现在它是一个100％基于Cairo绘制的图形工具库了（之前GTK+2.x时在2.8开始逐渐转向用Cairo绘制，但一直不彻底）。</p>
<p>这意味着两点：</p>
<ul>
<li>GTK+的一直以来评价不怎么样的跨平台性，在3.0将有显著的突破；</li>
<li>GTK+的Wayland后端，已经在路上了！</li>
</ul>
<p>见GTK+跑在Wayland上，截图引自：<a href="http://www.phoronix.com/scan.php?page=news_item&amp;px=ODQ1MQ">Kristian Shows Off GTK+ 3.0 On Wayland</a></p>
<p><a href="http://imtx.me/static/uploads/2010/11/gtk-and-wayland.jpeg"><img src="assets/gtk-and-wayland.jpeg" alt="Wayland and GTK+" /></a></p>
<p>当然，Qt也有了，限于篇福，这里就不介绍了。</p>
<p>另外一个已经在主开发分支便支持Wayland的东西便是：<a href="http://www.ibentu.org/2010/11/tag/clutter">Clutter</a>。这是一个基于OpenGL的动画框架，我以前介绍过很多次的<a href="http://imtx.me/tag/gnome-shell/">GNOME Shell</a>、<a href="http://www.ibentu.org/2010/11/2009/07/10/moblin-2-0-beta-media.html">Moblin</a>， 都是基于Clutter的。在Clutter当前1.5.x的开发分支，Wayland作为其中一个“backend”，已经得到了 “experimental”的支持。所以说，GNOME 3.0、MeeGo Netbook很可能会成为第一个应用Wayland的桌面环境。</p>
<p>那么，看来Wayland真的触手可及了啰？可以这么说，但是还差一点。</p>
<p><span style="color: #993300;"><strong>Wayland技术实现及工作重点</strong></span></p>
<p>Wayland的核心协议已经实现的差不多了，它充分利用了Linux内核的KMS、GEM、DRM等技术，另外，它默认是支持3D加速的，也就是通过OpenGL ES进行图形的合成——光是这一点，X Window又要泪奔了。</p>
<p>使用OpenGL ES这个子集而非OpenGL，这意味着什么？想想有多少项目是用OpenGL ES的：Android、iOS、WebOS、WebGL……几乎所有主流的的移动操作系统、浏览器3D的实现，都选用了精简、高效的OpenGL ES。</p>
<p>我不知道当前Android的Display Server、Input/Output是如何实现的，总之跟iOS相比，在触控的响应上是有差距的。未来，对OpenGL ES有着良好支持的Wayland，不知道会不会给这些基于Linux内核的移动操作系统发力呢？我想是非常有可能的！</p>
<p>这时问题就来了，因为Wayland所使用的，都是当前Linux下最新潮的图形技术。所以理所当然的，在驱动这一层面会有一些厂商跟不上。</p>
<p>拿nVIDIA开刷吧，KMS技术都出来一年多了，Intel的全部显卡和AMD部分显卡已经获得支持了，可nVIDIA压根就没有兴趣搞这个，以 致于开源社区利用反向工程，通过“Nouveau”项目让nVIDIA支持了KMS，当然比较遗憾的是，性能跟官方闭源的驱动是差了相当的距离。</p>
<p>所以说，基于Wayland的Linux桌面/移动要真正得到应用，驱动这一关是一定要解决的。不过正所谓潮流不可档，nVIDIA迟早会支持这项技术的。</p>
<p>等到驱动完全不成问题了，Wayland还需要一个全功能的“Compositor”，这个角色，就由Clutter/Mutter、 Compiz、KWin等当前主流的窗口管理器来扮演的，相信只要通过简单的修改，这些合成窗口管理器很快地就能转变成一个全能的“Wayland Compositor”！</p>
<p><span style="color: #993300;"><strong>把玩Wayland及展望未来</strong></span></p>
<p>讲了这么多技术、历史和业界，大家肯定枯燥了，究竟现在有没有可以跑的“Wayland Compositor”可以玩玩呢？当然！</p>
<p>现在，只要你从<a href="http://cgit.freedesktop.org/wayland">官方</a>取得源码，然后根据<a href="http://wayland.freedesktop.org/building.html">教程</a>进 行编译，就能跑起一个简单实现的“Wayland Compositor”。由于Wayland协议的灵活性，Wayland Compositor也可以拥有自己的后端：比如直接在DRM上跑Wayland（不需要X），或者在X Window上跑起一个Wayland Compositor（相当于在X Window上用Xephyr再跑一个X Window）。</p>
<p>当前我在Ubuntu 10.10的图形环境下，就跑起了默认的这个简易的Wayland Compositor，几点说明：</p>
<ul>
<li>支持透明、阴影和简单的窗口管理；</li>
<li>所有的图形绘制，都是通过Cairo-gl（Cairo的OpenGL后端）进行；</li>
</ul>
<p><a href="http://imtx.me/static/pictures/2010/11/wayland-picture-and-drag-drop.png"><img src="assets/wayland-picture-and-drag-drop.png" alt="Wayland Terminal" width="550" /></a></p>
<p>这是又一个例子，我编译了Clutter的Wayland后端，成功地跑起了一个Clutter的Demo：即同中Ubuntu Tweak的3D Logo。</p>
<p><a href="http://imtx.me/static/pictures/2010/11/wayland-clutter.png"><img src="assets/wayland-clutter.png" alt="Wayland and Clutter" width="550" /></a></p>
<p>除了这个Wayland Compositor本身是跑在X Window之上，其本身合成效果、处理窗口布局等等，都完全没有用到X，而且整个代码非常简洁。未来的Linux图形，就会像是这样一个结构简单又高效的样子。</p>
<p>相信看完我这些介绍，大家对Wayland是个什么角色，已经比较清楚了吧？</p>
<p>简单的说，它就是一个去除X Window中不必要的设计、充分利用现代Linux内核图形技术的一个显示机制，它的出现是自然而然的，它的使命不是为了消灭X Window，而是将Linux的图形技术发挥至更高的一个境界。传统的X Window（即经典X应用、Gtk 1.x/2.x等旧应用），也会在相当长一段时间内得到继续支持，通过Wayland Client的形式跑在Wayland Compositor上，直到最终升级、取代或被淘汰。</p>
<p>2011年后期或2012年，我们将能看到Wayland正式着陆，期待吧！</p>
<p><a href="http://www.ibentu.org/tag/wayland">Wayland</a>是什么呢？它是X Window？还是要取代X Window？它的优势在哪里？Linux桌面/移动会因此有什么变化？在本篇中，我将回顾历史，展望未来，通过简易的文字，来先回顾一下X Window，从而继续解答Wayland。</p>
<p>注：在下对X Window的理解仅限于表面，文章中会有不少技术、历史方面的错误，若有大侠指出，不胜感激！</p>
