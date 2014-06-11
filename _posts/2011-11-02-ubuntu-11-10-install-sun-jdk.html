---
layout: post
title: Ubuntu 11.10 开发环境配置 Install Sun JDK
categories:
- JAVA
- LINUX
tags:
- Java
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
<p>刚升级到了 Ubuntu 11.10 ,一切都挺让人满意的, 登录界面不一样拉, Ambiance主题也进行了微调, 很多小细节发生了变化, 比如现在的Terminal让我觉得相当舒服. Dash 图标和界面有改良, Dash 框不会在鼠标 over的时候弹出了；窗体按钮, 最大化,关闭什么的也很聪明的默认隐藏了； 软件中心升级, 很赞 ... ...</p>
<p>不过一升级完成就发现, 之前的 DesktopNova 和 自定义鼠标都用不了了. 这到还不是大问题, 可以刚准备开发, 才发现 Sun-java6 都消失了 -_-||</p>
<h3><span style="color: #993300;"><strong>安装SUN-JAVA6-JDK</strong></span></h3>
<p>之前写过 <a title="Ubuntu 10.10 开发环境配置 （三）Install Sun JDK" href="http://www.from0to1.net/ubuntu-10-10-%e5%bc%80%e5%8f%91%e7%8e%af%e5%a2%83%e9%85%8d%e7%bd%ae-%ef%bc%88%e4%b8%89%ef%bc%89install-sun-jdk/" target="_blank">Ubuntu 10.10 开发环境配置 （三）Install Sun JDK</a> , 但现在当然有些不一样了. 不过还好, 还是比较简单.</p>
<pre class="brush:shell">sudo add-apt-repository ppa:ferramroberto/java
sudo apt-get update
sudo apt-get install sun-java6-jdk sun-java6-plugin sun-java6-source</pre>
<p>&nbsp;</p>
<h3><span style="color: #993300;"><strong>配置默认JDK</strong></span></h3>
<p>安装完后，先看看目前使用的到底是哪个JDK？</p>
<pre class="brush:shell">java -version</pre>
<p>如果还是OpenJDK，那么可以用下面的命令来配置默认的JDK：</p>
<pre class="brush:shell">sudo update-alternatives --config java</pre>
<p>如果上面的命令，提示你只有一个可选的JDK，那么我们先查看目前的配置是什么:</p>
<pre class="brush:shell">update-alternatives --verbose --query java

<code>Link: java
 Status: auto
 Best: /usr/lib/jvm/java-6-openjdk/jre/bin/java
 Value: /usr/lib/jvm/java-6-openjdk/jre/bin/java</code></pre>
<p><code>Alternative: /usr/lib/jvm/java-6-openjdk/jre/bin/java<br />
Priority: 1061<br />
Slaves:<br />
java.1.gz /usr/lib/jvm/java-6-openjdk/jre/man/man1/java.1.gz</code></p>
<p>然后我们要做的就是手工的把安装的JDK添加到系统中：</p>
<pre class="brush:shell">sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/sun-java6-jdk/jre/bin/java 1701</pre>
<p>注意 "1061" 和我们手工更改的 "1701"</p>
<p>很显然, 11.10 还有更多的问题,等着呢,不过真希望不要太多~</p>
