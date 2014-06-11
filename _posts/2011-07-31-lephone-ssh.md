---
layout: post
title: LePhone 3GC101 穿越 SSH
categories:
- PHONE
tags:
- Android
- SSH
status: publish
type: post
published: true
meta:
  _wp_old_slug: lephone
author:
  login: villim
  email: villim@126.com
  display_name: Villim
  first_name: Villim
  last_name: Wong
---
<p>如果有SSH账户，可以很自由的飞跃长城。手机上也可以做到。比起 VPN 来，SSH的非全局代理让我感觉更舒服一些。</p>
<p>我目前使用的手机是 <strong>LePhone 3GC101, Android 2.2.1</strong> 系统。LePhone的系统是定制的，割版系统，想要飞跃长城。</p>
<h3><span style="color: #008000;">1. 首先要做的是必须获得ROOT权限</span></h3>
<p><strong>z4root</strong> 可以为 LePhone 解锁，同时可以装两个管理工具 <strong>Root Explorer</strong> 和 <strong>Superuser</strong>。</p>
<p>但是只是做完这些 还不足够，联想还删掉一些东西，需要手工恢复：</p>
<p>保证下面的路径中有对应的文件 （可以到这里<a href="http://bbs.lephone.cc/thread-95200-1-1.html" target="_blank">下载</a>）：</p>
<pre class="brush:shell">/system/framework/com.google.android.maps.jar
/system/etc/permissions/com.google.android.maps.xml
/data/app_s/NetworkLocation.apk</pre>
<p>给文件都设置正确权限：</p>
<p><img class="alignnone" title="Set Google Files Properties" src="assets/5996258577_151383262f.jpg" alt="" width="214" height="447" /></p>
<h3 class="brush:shell"><span style="color: #008000;">2. 安装SSHTunnel</span></h3>
<p>配置很简单，首先是 Host，Account</p>
<p><img class="alignnone" title="SSHTunnel Configuration" src="assets/5996499135_8265743c79.jpg" alt="" width="214" height="447" /></p>
<p>接下来是 Port Forwarding：</p>
<p><img class="alignnone" title="SSHTunnel Configuration" src="assets/5996678710_4166aa6804.jpg" alt="" width="214" height="447" /></p>
<p>Feature Setting 里面，可以对让指定的程序使用代理（Individual Proxy）</p>
<p><img class="alignnone" title="Individual Proxy Setting" src="assets/5997086754_a3cbd11e89.jpg" alt="" width="214" height="447" /></p>
<p>配置完成乐，只需要打开 “Tunnel Switch” 就搞定了。</p>
