---
layout: post
title: Threads in Bash
categories:
- LINUX
tags:
- Bash
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
<p>The title 'Threads in Bash' is incorrect ^_^ There's no thread when creating BASH Script, I just find out these days when I trying to make a script to update ZIMBRA accounts by Bash.</p>
<p>Recently when we creating scripts in linux, most people will choose Python and few person will use Perl. But why I use BASH this time ... ???  ^o^ In fact, I don't know, maybe just cause it's a little funny to use some Bash some time. And I really quite enjoyed in that time. And At the beginning, I didn't think will make a so sophisticated script at the end.</p>
<p>After finished the first version, I find there's so many accounts, so if the script can't be continuable, it's unacceptable. After that, it's too slow to update, costing few days. So make it able to run with several threads is a good idea. However, I have said, there's no Threads in BASH, what a awkward ...</p>
<p>The only choose is using multiple processes, and infact it's quite easy to do it, just like:</p>
<pre class="lang:sh decode:true ">COMMAND A &amp; COMMAND B &amp; COMMAND C &amp; 
WAIT</pre>
<ul>
<li><span style="color: #ff0000;"><strong>&amp;</strong></span>  as we know, it means the process is forked and shell will run it in the backend in a sub shell</li>
<li>and <span style="color: #ff0000;"><strong>WAIT</strong></span> will make sure waiting for  all the processes to finish</li>
</ul>
<p>P.S.</p>
<p>However, after finished these scripts. It's still not good enough. It's still too slow.</p>
<p>And even using real thread can't help too much. The time cost mostly in the cmd tool ZMPROV provided by Zimbra.</p>
<p>So the best way could be creating you own ZMPROV  wapper, then you can do batch update and avoid wasting time in creating and release session.</p>
