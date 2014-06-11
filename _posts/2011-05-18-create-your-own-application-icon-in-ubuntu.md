---
layout: post
title: Create Your Own Application Icon in Ubuntu
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
<h2><span style="color: #008000;">1. Prepare the software you want</span></h2>
<p>e.g. I download spring development tool suit</p>
<h2><span style="color: #008000;">2. Make it able to run in bash</span></h2>
<pre class="brush:shell">sudo ln -s ~/springsource/sts-2.6.1.RELEASE/STS /usr/bin/sts</pre>
<h2><span style="color: #008000;">3. Create application icon</span></h2>
<pre class="brush:shell">cd /usr/share/applications
sudo vim STS.desktop</pre>
<p>add following text:</p>
<pre class="brush:plain">[Desktop Entry]
Name=sts
GenericName=STS
Commen=Spring Tools Suit
Exec=/usr/bin/sts
StartupNotify=true
Terminal=false
Type=Application
Icon=/home/villim/Tools/springsource/sts-2.6.1.RELEASE/icon.xpm
Categories=Development;IDE;</pre>
<h2><span style="color: #008000;">4. Make application run when system startup</span></h2>
<p>like tomboy, if you wanna automatically run it when system startup.just go :</p>
<p>System --&gt; Preferences --&gt; Startup Applications</p>
