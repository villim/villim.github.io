---
layout: post
title: 使用 AutoSSH
categories:
- LINUX
tags:
- SSH
- Ubuntu
status: publish
type: post
published: true
meta:
  _wp_old_slug: ''
author:
  login: villim
  email: villim@126.com
  display_name: Villim
  first_name: Villim
  last_name: Wong
---
<p>用了SSH有一个很麻烦的事情就是链接时不时会断掉 ... 唉 重新链接输入密码也是相当麻烦的事情。</p>
<p>所以尝试以下 AutoSSH，使用方法和 <acronym title="Secure Shell">SSH</acronym> 类似，只是它提供了断线自动连接功能，这样就不必每次重新输入命令了。</p>
<p>安装：</p>
<pre class="brush:shell">udo apt-get install autossh</pre>
<p>使用：</p>
<pre class="brush:shell">autossh -M 2000 -N -v  username@hostip -D 127.0.0.1:7070</pre>
