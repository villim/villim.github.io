---
layout: post
title: Character Encoding Note
categories:
- OTHER
tags:
- Encoding
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
<p>工作的关系，处理XML不可识别字符的问题，于是花了不少时间研究UTF-8,也就不得不大致把字符编码(Character Encoding)的知识给顺了一遍。<br />
毫无疑问字符编码是计算机的基础中的基础知识，没有正确理解它一定迟早会在程序设计中陷入泥潭。借着个机会就把字符编码的概念整理以下，希望能把一直模模糊糊的概念变得稍微清晰了一点。</p>
<p>首先我们需要知道的是，计算机只能识别二进制的字符串，每个Bit只有0和1两个状态。所以所有的字符编码最终都是和二进制做对应的。</p>
<h2><span style="color: #008000;">ASCII码</span></h2>
<p><span style="color: #993300;"><strong>ASCII</strong></span> (American Standard Code for Information Interchange) 是基于现代英语的编码。<br />
即使到今天它仍是最通用的单字节编码系统。单字节即是一个Byte。一共能够表示在256个符号，即0000 0000 - 1111 1111. 目前的 ASCII 码一共定了128个字符编码，33个控制字符。<br />
作为计算机刚在美国兴起而定制的编码规范，毫无疑问它成功解决了美国人（西方人）使用计算机的问题。可当全球计算机普及的时候，一切西欧字符，亚洲语言字符便无能为力了。</p>
<h2><span style="color: #008000;">基于 ASCII 的编码</span></h2>
<p><strong><span style="color: #993300;">ISO 8859-1</span> ：</strong> 又叫 Latin-1 或者 “西欧语言”。它在ASCII的基础上，在空置的0xA0-0xFF的范围内，加入了96个字母及符号，供使用附加符号的拉丁字母语言使用。</p>
<p><strong><span style="color: #993300;">      GB2312</span> :</strong>      使用两个字节表示一个汉字，一个“高位字节”，一个“低位字节”，所以理论上最多可以表示 256 X 256 = 65536 个字符。GB2312 的出现，基本满足了汉字的基本需要，但是对于人名，古汉语中出现的罕用字无能为力，这导致后来的GBK和GB18030汉字字符集的出现。（注意 GBK 和 GB18030 不是扩展ASCII）</p>
<p>非ASCII码的问题，用中文来举例，中文字没有真正属于自己的编码。因为扩展ASCII码虽然没有真正的标准化，但是PC里的ASCII码还是有一个事实标准的（存放着英文制表符），所以很多软件利用这些符号来画表格。这样的软件用到中文系统中，这些表格符就会被误认作中文字，破坏版面。而且，统计中英文混合字符串中的字数，也是比较复杂的，我们必须判断一个ASCII码是否扩展，以及它的下一个ASCII是否扩展，然后才“猜”那可能是一个中文字 。</p>
<p>所以用扩展ASCII码的方式不能解决所有的语言编码问题，将所有国家所有文字，法文，德文，中文，日文，韩文 ...  统一起来的解决方案就是 Unicode。（注：GB类的汉字编码虽然也使用多字节编码，但是和Unicode毫无关系。）</p>
<h2><span style="color: #008000;">Unicode</span></h2>
<p>在Unicode中所有字符都有惟一的编码。比如汉字不再使用“两个扩展ASCII”，而是使用“1个Unicode”。Unicode有两套标准，一套叫UCS-2(Unicode-16)，用2个字节为字符编码，另一套叫UCS-4(Unicode-32)，用4个字节为字符编码。</p>
<p>看起来Unicode非常完美了，为什么不能所有的系统都开始使用Unicode呢？<br />
因为Unicode也有很严重的问题。在ASCII码里面用一个Byte表示的字符，现在至少需要2个Byte。比如“A”的ASCII是65，而Unicode是0065。这不仅是存储空家的浪费。而且以前所有基于ASCII编码的字符处理程序都不能再正常工作。我们是不可能替换调已经使用了几十年的所有代码的。</p>
<p>怎么办呢？我们有对Unicode的需求，却似乎不能让他真实的在现实环境中使用？ Unicode 虽然对字符编码作出了规范，但是没有说明应该如何存储。于是 UTF 出现了。</p>
<h2><span style="color: #008000;">UTF  (UCS Transformation Format)</span></h2>
<p>它是将Unicode编码规则和计算机的实际编码对应起来的一个规则。现在流行的UTF有2种：UTF-8 和 UTF-16。UTF-16和Unicode编码规则是一致的。需要看看的是UTF-8.</p>
<h2><span style="color: #008000;">UTF-8</span></h2>
<p>UTF-8只是Unicode的实现方法之一！！它的特点是它是变长编码。直接用图表来表示比较明显：</p>
<pre class="brush:plain">Bits | Last code point| Byte 1   Byte 2   Byte 3   Byte 4   Byte 5   Byte 6
7    |  U+007F        | 0xxxxxxx
11   |  U+07FF        | 110xxxxx 10xxxxxx
16   |  U+FFFF        | 1110xxxx 10xxxxxx 10xxxxxx
21   |  U+1FFFFF      | 11110xxx 10xxxxxx 10xxxxxx 10xxxxxx
26   |  U+3FFFFFF     | 111110xx 10xxxxxx 10xxxxxx 10xxxxxx 10xxxxxx
31   |  U+7FFFFFFF    | 1111110x 10xxxxxx 10xxxxxx 10xxxxxx 10xxxxxx 10xxxxxx</pre>
<p>不过到目前为止，大部分情况都只用到3个Byte。看一个例子：<br />
已知“严”的unicode是4E25（100111000100101），根据上表，可以发现4E25处在第三行的范围内（0000 0800-0000 FFFF），因此“严”的UTF-8编码需要三个字节，即格式是“1110xxxx 10xxxxxx 10xxxxxx”。然后，从“严”的最后一个二进制位开始，依次从后向前填入格式中的x，多出的位补0。这样就得到了，“严”的UTF-8编码是 “11100100 10111000 10100101”，转换成十六进制就是E4B8A5。<br />
可能你已经注意到了，E4B8A5 和 Unicode 的 “4E25”  并不一致，他们之间需要程序转换。</p>
<h2><span style="color: #008000;">UTF的字节序问题</span></h2>
<p>UTF -8以字节为编码单元，没有字节序的问题。UTF-16以两个字节为编码单元，就存在字节序的问题。如同之前所说，Unicode 只是规范了规则，并没有说明如何存储。例如收到一个“奎”的Unicode编码是594E，“乙”的Unicode编码是4E59。如果我们收到UTF-16字节流“594E”，那么这是“奎”还是 “乙”？ 存储的时候，4E在前，59在后，就是 <em><strong>Big endian </strong></em>方式；58在前，4E在后，就是 <em><strong>Little endian </strong></em>方式。<br />
接下来的问题是，计算机如何知道你采用了什么方式呢？Unicode规范中推荐的标记字节顺序的方法是 <em><strong>BOM （Byte Order Mark）</strong></em>。在UCS 编码中有一个叫做 " <em>ZERO WIDTH NO-BREAK SPACE </em>" 的字符，它的编码是 FEFF。而 FFFE 在UCS中是不存在的字符，所以不应该出现在实际传输中。UCS规范建议我们在传输字节流前，先传输字符 "<em>ZERO WIDTH NO-BREAK SPACE</em>"。这样如果接收者收到FEFF，就表明这个字节流是Big-Endian的；如果收到FFFE，就表明这个字节流是Little-Endian的。因此字符"ZERO WIDTH NO-BREAK SPACE"又被称作BOM。</p>
<p><strong>该说的说得差不多了，做一个练习：</strong></p>
<p>使用Windows记事本的“另存为”，可以在GBK、Unicode、Unicode big endian和UTF-8这几种编码方式间相互转换。同样是txt文件，Windows是怎样识别编码方式的呢？</p>
