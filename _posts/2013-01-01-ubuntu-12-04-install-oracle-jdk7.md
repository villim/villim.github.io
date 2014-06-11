---
layout: post
title: Ubuntu 12.04 开发环境配置 Install Oracle JDK7
categories:
- JAVA
- LINUX
tags:
- Java
- Java7
- Linux
- Ubuntu
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
<p>自从 Java 跑到 Oracle 以后，安装 JDK 变得很讨厌， 还好有好心人有好心人给大家提供 PPA</p>
<pre class="brush:shell">sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
sudo apt-get install oracle-java7-installer</pre>
<p>说起来这台老机器因为显卡分辨率得关系，没办法升到最新版，Ubuntu又不再支持12.04了，还真是蛋疼啊～ 可惜又不想在虚拟机上玩 Linux ，真是麻烦。</p>
