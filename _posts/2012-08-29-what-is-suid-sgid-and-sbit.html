---
layout: post
title: What is SUID,SGID and SBIT
categories:
- LINUX
tags:
- Linux
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
<p>之前改写用 Maven 来做 RPM 包，碰到了很多需要设置权限 “2755” 的情况。简单的查过以后一直还是糊里糊涂，不幸有同事来刨根问底，终于下决心把这个事情彻底整理一下。</p>
<h3><span style="color: #993300;"><strong>Sticky Bit ( SBIT )</strong></span></h3>
<p>在Unix刚开始的年代，计算机的资源是有限的，可不像现在人人都玩着自己的机器。Unix 的基本概念就是多人多任务的操作系统，为了在CPU、内存有限的情况下，提高使用体验。有一些共用的程序，我们期望在第一个用户载入以后就不要释放，那么我们就可以给它设置 Sticky Bit。</p>
<p>不过现在只有很少的Unix版本在继续使用这个概念，目前最常用的使用方法是在文件夹上设置 Sticky Bit。</p>
<pre class="brush:shell">villimw@Wall-E:~/WORK$ ls -ld Test/
drwxr-sr-x 2 villimw villimw 4096 2012-08-29 22:47 Test/
villimw@Wall-E:~/WORK$ chmod +t Test/ ; ls -ld Test/
drwxr-sr-t 2 villimw villimw 4096 2012-08-29 22:47 Test/</pre>
<p>在没有 SBIT 时，任何用户拥有 write 和 excute 权限都可以 rename 或者 delete 文件夹内的文件。而在 SBIT 设置后，只有文件的 owner，目录的 owner 或者 superuser 才可以 rename 或者 delete 文件夹内的文件。</p>
<p>在系统里的 /tmp 目录默认就设置了 SBIT：</p>
<pre class="brush:shell">villimw@Wall-E:~/WORK$ ls -ld /tmp
drwxrwxrwt 19 root root 20480 2012-08-30 02:17 /tmp</pre>
<h3></h3>
<h3><span style="color: #993300;"><strong>SUID</strong></span></h3>
<p>SUID 的含义是 Set UID, 你会在 owner 权限组里面看到奇怪的 “s”。比如 passwd 就默认有这个权限。</p>
<pre class="brush:shell">villimw@Wall-E:~/WORK/Test$ ll /usr/bin/passwd 
-rwsr-xr-x 1 root root 37100 2011-02-14 17:12 /usr/bin/passwd*</pre>
<p>它的含义是，任何用户，执行 passwd 的时候，都可以以 root 的身份操作。如果没有 SUID ，那么你必须使用 sudo 来操作。那么这样直接把执行文件的用root权限暴露给所有用户，不是增加了系统的不安全吗？（你的答案是？）</p>
<p>SUID 仅用在 binary program上，不能在shell script上使用。</p>
<pre class="brush:shell">chmod  u+s</pre>
<h3></h3>
<h3><span style="color: #993300;"><strong>SGID</strong></span></h3>
<p>SGID 和 SUID 的含义是差不多的，只不过把这个 “s” 放到了 group 权限组里面。而且它仅对目录和文件有效。</p>
<p>若在目录上设置了 SGID，只要使用者在该目录又写入权限。那么该使用者在此目录新建的任何文件，将会得到和目录相同的 owner 和 permission。</p>
<pre class="brush:shell">chmod g+s</pre>
<p>&nbsp;</p>
<p>设置权限除了使用 u+s ; g+s 这样的字符串，当然也可以使用数字：</p>
<ul>
<li>4 -&gt; SUID</li>
<li>2 -&gt; SGID</li>
<li>1 -&gt; SBIT</li>
</ul>
