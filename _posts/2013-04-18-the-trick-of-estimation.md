---
layout: post
title: 估算的基础
categories:
- NOTES
- OTHER
tags:
- Book
- Review
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
<p>年初读的《这也能想到？》是一本关于大数据的书。不过，这个大数据可不是Big Data。对于大多数 “世界性” 问题，虽然有时看来荒缪又无厘头，比如说，此时此刻有多少人正在上厕所？ ... 不过有些问题到也有着实实在在的意义，随便想想就可以随意列出好些问题来，譬如：如果石油耗尽，我们需要修建多少个核电站才能维持目前的生活和生产？ 50年后每个中国人拥有几套房产？</p>
<p>估算其实是一个基本技能，有助于你理解这个世界和做出正确的决策。这也是很多大公司喜欢考察的。即便这些都不重要，尝试着回答这类问题本身也是很有趣的。</p>
<h4><span style="color: #993300;"><strong>科学计数法</strong></span></h4>
<p>要把估算做好，还是有一些基本的方法。首先应该学会使用科学计数法，很简单如果用 100 000 000 才表示1亿，不可能有 10<sup>8</sup> 来的清晰明了。 x * 10<sup>y</sup> 这样的科学计数法表达方式，我们关注的更多是指数y，而不是系数 x。</p>
<ul>
<li><span style="line-height: 1.6em;">乘法：系数相乘，指数相加</span></li>
<li><span style="line-height: 1.6em;">除法：系数相除，指数相减</span></li>
<li><span style="line-height: 1.6em;">加法：保证指数相同，系数相加</span></li>
<li><span style="line-height: 1.6em;">减法：保证指数相同，系数相减</span></li>
</ul>
<p>&nbsp;</p>
<h4><span style="color: #993300;">单位换算</span></h4>
<p>日常生活中使用的单位，和公制单位常常是不一致的，最好将常用换算备案，随身携带，以便查找。</p>
<table border="1" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td valign="top" width="197"> 量</td>
<td valign="top" width="197"> 公制</td>
<td valign="top" width="197"> 美国常用单位</td>
</tr>
<tr>
<td valign="top" width="197"> 1(m)</td>
<td valign="top" width="197"> 1米（m）</td>
<td valign="top" width="197"> 3英尺（ft）</td>
</tr>
<tr>
<td valign="top" width="197"> 。。。</td>
<td valign="top" width="197"> 。。。</td>
<td valign="top" width="197"> 。。。</td>
</tr>
</tbody>
</table>
<p>当然还要熟悉单位换算的规则，参考下面两个列子搞清楚换算的方法：</p>
<ul>
<li><span style="line-height: 1.6em;">1年 = 1年 x ( 365天/1年 ) ( 24小时/1天) (60分钟/1小时) (60秒/1分钟) = 3.15 x 10</span><sup style="line-height: 1.6em;">7</sup><span style="line-height: 1.6em;"> s</span></li>
<li><span style="line-height: 1.6em;">1 m/s = 1m/s x (1km/ 10^3 m) (0.6 mi/1km) (1/) (0.6 mi/1 km) x (60秒/1分钟) (60分钟/1小时) = 2.2 mi/h</span></li>
</ul>
<p>&nbsp;</p>
<h4> <span style="color: #993300;"><strong>估算的技巧</strong></span></h4>
<p>这篇本来是准备写 “技巧”的，可是实在是很不好写，如果真的写出来，似乎完全就是本书了。</p>
<p>算了，这个就到这儿了，掌握了基本的知识，估算最重要的还是思考和不断的练习。</p>
