---
layout: post
title: What is Digital Certification
categories:
- LINUX
- OTHER
tags:
- HTTPS
- SSH
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  _wp_old_slug: what-is-certification
author:
  login: villim
  email: villim@126.com
  display_name: Villim
  first_name: Villim
  last_name: Wong
---
<p>之前做 Knowledge Share 的时候，整理了一下关于证书的东西，再精简一个文字版放这儿归档。</p>
<p>要说证书是什么似乎是太常见了，之前说  <a title="A Little HTTP" href="http://www.from0to1.net/a-little-http/" target="_blank">A Little HTTP</a> 的时候提到的 HTTPS; 还有说起 <a title="SSH Proxy" href="http://www.from0to1.net/ssh-proxy/" target="_blank">SSH</a> 也少不了证书。IE 里面的 "证书管理器" 估计你多少都曾经看到过了。可是要说证书是什么，明白肯定明白，不过似乎又有些说不清，道不明的样子。整理清楚什么是证书先需要先从 Key 说起。</p>
<h4><strong><span style="color: #993300;">Public Key &amp; Private Key</span></strong></h4>
<p><em>用过 SSH 的人必然知道这两个东西了，他们的用处是什么呢？</em></p>
<div>
<ul>
<li><em><span style="color: #808000;">Keys are used to encrypt information.</span></em></li>
<li><em><span style="color: #808000;">Encrypting information means "scrambling it up"</span></em></li>
<li><em><span style="color: #808000;">So that only a person with the appropriate key can make it readable again</span></em></li>
<li><em><span style="color: #808000;">Either one of the two keys can encrypt data, and the other key can decrypt it</span></em></li>
</ul>
<p><em>比如 Bob 有这两把 Key，然后他将 Public Key 交给 Susan，那么Susan 就可以把发给 Bob 的消息用 Public Key 加密了。比如下面的信息：</em></p>
<p><em><strong>"Hey Bob, how about lunch at Taco Bell. I hear they have free refills!"</strong></em></p>
<p><em>用 public key 加密后，得到：</em></p>
<p><em><strong>HNFmsEm6Un BejhhyCGKOK JUxhiygSBCEiC 0QYIh/Hn3xgiK lxx2lCFHDC/A</strong></em></p>
<p><em>而 Bob 收到消息以后，能且只能用 Private Key  将信息还原。知道 encrypt / decrypt ，再看看数字签名是什么。</em></p>
<h4><span style="color: #993300;"><strong>Digital Signature</strong></span></h4>
<div>
<ul>
<li><em><strong>1.</strong> With his private key and the right software,</em></li>
<li><em>Bob can <span style="color: #808000;"><strong>put</strong><strong> </strong><strong>digital</strong><strong> </strong><strong>signatures</strong><strong> </strong><strong>on</strong><strong> </strong><strong>documents</strong><strong> </strong><strong>and</strong><strong> </strong><strong>other</strong><strong> </strong><strong>data</strong></span></em></li>
<li><em><span style="color: #808000;"><strong><span style="color: #000000;">2.</span> A</strong><strong> </strong><strong>digital</strong><strong> </strong><strong>signature</strong><strong> </strong><strong>is</strong><strong> </strong><strong>a</strong><strong> </strong><strong>"stam</strong><strong>p"</strong></span><strong> </strong></em></li>
<li><em>Bob places on the data which is unique to Bob, and is very difficult to forge</em></li>
<li><em><strong>3.</strong> In addition, the <span style="color: #808000;"><strong>signature</strong><strong> </strong><strong>assures</strong></span><strong> </strong>that <span style="color: #808000;"><strong>any</strong><strong> </strong><strong>changes</strong></span><strong> </strong>made <span style="color: #808000;"><strong>to the data</strong></span></em></li>
<li><em>that has been signed <span style="color: #808000;"><strong>can</strong><strong> </strong><strong>not</strong><strong> </strong><strong>go</strong><strong> </strong><strong>undetected</strong></span></em></li>
</ul>
</div>
<p><em>所以要得到数字签名分 3 步走：</em></p>
<ol>
<li><em>使用 SHA 或者 MD5 之类的算法，生成文件的数字摘要</em></li>
<li><em>将生成的数字摘要, 用 Private Key 做 Encrypt , 即可得到 Signature</em></li>
<li><em>然后将 Signature 附加到原消息上即可</em></li>
</ol>
<p><em>证书的 decrypt 操作本身保证了文件来自正确的地方，因为只有对应的 Public Key 能解开其 Private Key;  decrypt 后得到的 Message Digest 保证了信息是原封原样的, 因为我们只需要再生成新的 Digest，就可以和之前的作对比。</em></p>
<p><em>但是，这里有一个严重的问题：如果有人恶意的，比如悄悄替换了 Susan 本机上 Bob's Public Key , 那么这个人就可以假冒 Bob 继续和 Susan 通信了。所以我们还需要证书。</em></p>
<h4><span style="color: #993300;"><strong>Digital Certificate</strong></span></h4>
<p><em>数字证书是以 Public Key 为基础，加上一些附加信息组成的。比如 Bob's public key 再加上 Bob 的个人信息，和证书的有效期等组成证书的内容，对这个内容用 CA 的 Private Key 加密得到的就是 Digital Certificate 了。CA 的 public key 对所有的人都是开放的，而被封装的 Bob's Public Key 的有效性是由 CA 负责认证的。</em></p>
<p><em>使用时，我们只需要将 Digital Certificate 和之前的 Digital Signature 一起附加到原始信息里就可以了。和之前不同的是，需要从 Certificate 里面得到解开 Signature 的 Public Key.</em></p>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
