---
layout: post
title: A Little HTTP
categories:
- OTHER
tags:
- HTTP
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
<p>每天都在折腾新玩意儿，AJAX，REST，WebService ... 可是却没怎么认真关心过互联网兴起的基础: HTTP。或许应该仔细地看看这个熟悉的陌生人了。</p>
<h3><span style="color: #008000;"><strong>HTTP 简介</strong></span></h3>
<p>HTTP 是 <strong>Hyper Text Transfer Protocol</strong> 的缩写。它是基于应用层的通信规范。虽然通常提到HTTP都是指上网浏览网页，但是其实HTTP本身只是个协议，可不是只能用到浏览器上的。HTTP协议是由 <strong>W</strong>orld <strong>W</strong>ide <strong>W</strong>eb <strong>C</strong>onsortium 和 <strong>I</strong>nternet <strong>E</strong>ngineering <strong>T</strong>ask <strong>F</strong>orce 合作定义的。最出名的是目前普遍使用的 HTTP 1.1 (<a title="RFC 2616" href="http://tools.ietf.org/html/rfc2616" target="_blank">RFC 2616</a>) .</p>
<h3><span style="color: #008000;"><strong>HTTP 在网络协议中的位置</strong></span></h3>
<p><img class="alignnone" title="HTTP Layer" src="assets/6058172804_9074ff8bc5.jpg" alt="" width="396" height="300" /><br />
通常HTTP是在TCP层协议之上，默认的 HTTP 端口是80。可当它在TLS或者SSL协议层之上的时候，就是我们常说的 HTTPS了，默认的端口为443.  注意这里说的是“通常”，如同能在TLS或者SSL之上一样，HTTP并没有规定必须使用TCP协议。其实是可以使用其他协议的，比如 UDP (User Datagram Protocol) . Ok ，<a href="http://zh.wikipedia.org/wiki/%E7%94%A8%E6%88%B7%E6%95%B0%E6%8D%AE%E6%8A%A5%E5%8D%8F%E8%AE%AE" target="_blank">那么为什么不使用 UDP 呢？</a></p>
<p>&nbsp;</p>
<h3><strong><span style="color: #008000;">HTTP 如何工作</span></strong></h3>
<p>总的来说，HTTP协议永远都是客户端发起请求，服务器回送响应。无法实现在客户端没有发起请求的时候，服务器将消息推送给客户端. 它是一个无状态的协议，同一个客户端的这次请求和上次请求是没有对应关系。</p>
<p>一次HTTP操作称为一个事务，其工作过程可分为四步：<br />
<span style="color: #800000;"><strong>1）首先客户机与服务器需要建立连接</strong></span></p>
<p>比如打开一个网络地址，比如 <a href="http://www.from0to1.net/">http://www.from0to1.net/</a>，HTTP开始工作。</p>
<p>这里不能不提到的一个概念是 <span style="color: #ff6600;"><strong>TCP Three-way Handshake</strong></span> ：<br />
<img class="alignnone" title="TCP Three-way Handshake" src="assets/Connection_TCP.gif" alt="" width="525" height="451" /></p>
<p>TCP 三次握手, 也不是一两句能说清除的。可以参考<a title="TCP 三次握手" href="http://blog.chinaunix.net/space.php?uid=20587912&amp;do=blog&amp;cuid=2201855" target="_blank">这里</a>。</p>
<p><strong><span style="color: #800000;">2）建立连接后，客户机发送一个请求给服务器</span></strong></p>
<p>请求方式的格式为：统一资源标识符（URL）、协议版本号，后边是MIME信息包括请求修饰符、客户机信息和可能的内容。</p>
<p>以下时使用 Firefox 插件 <em><strong>Live HTTP Headers </strong></em>查看的内容。</p>
<pre class="brush:plain">GET / HTTP/1.1
Host: www.villim.net
User-Agent: Mozilla/5.0 (X11; U; Linux i686; en-US; rv:1.9.2.18) Gecko/20110615 Ubuntu/10.10 (maverick) Firefox/3.6.18
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-us,en;q=0.5
Accept-Encoding: gzip,deflate
Accept-Charset: ISO-8859-1,utf-8;q=0.7,*;q=0.7
Keep-Alive: 115
Cookie: wp-settings-1=m7%3Dc%26m5%3Do%26m6%3Dc%26m0%3Dc%26m8%3Dc%26m9%3Do%26hidetb%3D1%26editor%3Dtinymce%26m3%3Dc%26m2%3Do%26m1%3Do%26m4%3Do; wp-settings-time-1=1312254428
DNT: 1
Connection: keep-alive</pre>
<p><strong><span style="color: #800000;">3）服务器接到请求后，给予相应的响应信息</span></strong></p>
<p>其格式为一个状态行，包括信息的协议版本号、一个成功或错误的代码，后边是MIME信息包括服务器信息、实体信息和可能的内容。</p>
<pre class="brush:plain">HTTP/1.1 200 OK
Date: Fri, 19 Aug 2011 01:17:59 GMT
Server: Apache/2.2.19 (Unix) mod_ssl/2.2.19 OpenSSL/0.9.8e-fips-rhel5 mod_auth_passthrough/2.1 mod_bwlimited/1.4 FrontPage/5.0.2.2635 mod_perl/2.0.5 Perl/v5.8.8
X-Pingback: http://www.from0to1.net/xmlrpc.php
X-Powered-By: W3 Total Cache/0.9.2.3
Vary: Accept-Encoding
Keep-Alive: timeout=5, max=100
Connection: Keep-Alive
Transfer-Encoding: chunked
Content-Type: text/html; charset=UTF-8</pre>
<p><strong><span style="color: #800000;">4）客户端接收服务器所返回的信息通过浏览器显示在用户的显示屏上，然后客户机与服务器断开连接。</span></strong></p>
<p>如果在以上过程中的某一步出现错误，那么产生错误的信息将返回到客户端，有显示屏输出。对于用户来说，这些过程是由HTTP自己完成的，用户只要用鼠标点击，等待信息显示就可以了。</p>
<ul>
<li>1xx消息——请求已被服务器接收，继续处理</li>
<li>2xx成功——请求已成功被服务器接收、理解、并接受</li>
<li>3xx重定向——需要后续操作才能完成这一请求</li>
<li>4xx请求错误——请求含有词法错误或者无法被执行</li>
<li>5xx服务器错误——服务器在处理某个正确请求时发生错误</li>
</ul>
<p>更详细的代码对照可以查看<a title="HTTP 代码对照" href="http://zh.wikipedia.org/wiki/HTTP%E7%8A%B6%E6%80%81%E7%A0%81" target="_blank">这里</a>。</p>
<p>&nbsp;</p>
<h3><span style="color: #008000;">HTTP 请求方法</span></h3>
<p>HTTP/1.1协议中共定义了八种方法（有时也叫“动作”）来表明Request-URI指定的资源的不同操作方式：</p>
<p><strong><span style="color: #800000;">OPTIONS</span></strong><br />
<em>返回服务器针对特定资源所支持的HTTP请求方法。也可以利用向Web服务器发送'*'的请求来测试服务器的功能性。</em></p>
<p><span style="color: #800000;"><strong>HEAD</strong></span><br />
<em>向服务器索要与GET请求相一致的响应，只不过响应体将不会被返回。这一方法可以在不必传输整个响应内容的情况下，就可以获取包含在响应消息头中的元信息。</em></p>
<p><span class="Apple-style-span" style="color: #800000;"><strong>GET</strong></span><br />
<em>向特定的资源发出请求。注意：GET方法不应当被用于产生“副作用”的操作中，例如在Web Application中。其中一个原因是GET可能会被网络蜘蛛等随意访问。参见安全方法</em></p>
<p><span style="color: #800000;"><strong>POST</strong></span><br />
<em>向指定资源提交数据进行处理请求（例如提交表单或者上传文件）。数据被包含在请求体中。POST请求可能会导致新的资源的建立和/或已有资源的修改。</em></p>
<p><strong><span style="color: #800000;">PUT</span></strong><br />
<em>向指定资源位置上传其最新内容。</em></p>
<p><span style="color: #800000;"><strong>DELETE</strong></span><br />
<em>请求服务器删除Request-URI所标识的资源。</em></p>
<p><span style="color: #800000;"><strong>TRACE</strong></span><br />
<em>回显服务器收到的请求，主要用于测试或诊断。</em></p>
<p><span style="color: #800000;"><strong>CONNECT</strong></span><br />
<em>HTTP/1.1协议中预留给能够将连接改为管道方式的代理服务器。</em></p>
<p>方法名称是区分大小写的。当某个请求所针对的资源不支持对应的请求方法的时候，服务器应当返回状态码405（Method Not Allowed）；当服务器不认识或者不支持对应的请求方法的时候，应当返回状态码501（Not Implemented）。</p>
<p>HTTP服务器至少应该实现GET和HEAD方法，其他方法都是可选的。当然，所有的方法支持的实现都应当符合下述的方法各自的语义定义。此外，除了上述方法，特定的HTTP服务器还能够扩展自定义的方法。</p>
<p>&nbsp;</p>
<h3><span style="color: #008000;"><strong>持久链接</strong></span></h3>
<p>在 HTTP 0.9和1.0里，TCP链接在每一对 request和response之后就会关闭。 毫无疑问会有延迟的影响。而且对于每个这样的连接，TCP得在客户端和服务器端分配TCP缓冲区，并维持TCP变量。对于有可能同时为来自数百个不同客户的请求提供服务的web服务器来说，这会严重增加其负担。</p>
<p>所以在 HTTP 1.1中增加了 keep-alive-mechanism, 可以让connection再多次request中被重复使用。</p>
<h3><span style="color: #008000;"><strong>Cookie 和 Session</strong></span></h3>
<p>因为HTTP是无状态的，这给我们大量需要保持状态的WEB应用程序带来了麻烦，比如购物车。<strong> Cookie</strong> 和 <strong>Session</strong> 就是这个目的，用来保存客户端状态的机制。 Session可以用Cookie来实现，也可以用URL回写的机制来实现。</p>
<p>Cookie 和 Session 有以下明显的不同点：</p>
<ol>
<li><strong>Cookie 将状态保存在客户端，Session将状态保存在服务器端</strong></li>
<li><strong>Cookies 是服务器在本地机器上存储的小段文本并随每一个请求发送至同一个服务器</strong></li>
</ol>
<p>Cookie最早在RFC2109中实现，后续RFC2965 做了增强。网络服务器用HTTP头向客户端发送cookies，在客户终端，浏览器解析这些cookies并将它们保存为一个本地文件，它会自动将同一服务器的任何请求缚上这些cookies。Session并没有在HTTP的协议中定义.</p>
<p>Session 是针对每一个用户的，变量的值保存在服务器上，用一个sessionID来区分是哪个用户session变量,这个值是通过用户的浏览器在访问的时候返回给服务器，当客户禁用cookie时，这个值也可能设置为由get来返回给服务器。 就安全性来说：当你访问一个使用session 的站点，同时在自己机子上建立一个cookie，建议在服务器端的SESSION机制更安全些，因为它不会任意读取客户存储的信息。</p>
<p>&nbsp;</p>
<p><span style="color: #008000;"><strong>HTTPS 图解</strong></span></p>
<p>从上面的图，已经可以看到，HTTPS就是加上了信息加密的处理。下面这个图已经能很明白的展示了。</p>
<p><img class="alignnone" title="HTTPS " src="assets/6078438335_9a974ef092.jpg" alt="" width="500" height="432" /></p>
<p>关于 数字签名 的概念，请参考 <a title="图解数字签名" href="http://www.ruanyifeng.com/blog/2011/08/what_is_a_digital_signature.html" target="_blank">这里</a>。</p>
