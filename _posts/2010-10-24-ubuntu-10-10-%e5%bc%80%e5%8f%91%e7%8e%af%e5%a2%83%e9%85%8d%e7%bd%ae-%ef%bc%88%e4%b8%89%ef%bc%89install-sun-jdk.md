---
layout: post
title: Ubuntu 10.10 开发环境配置 （三）Install Sun JDK
categories:
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
<p>和大多数Linux一样，一般默认安装的Open JDK，如果你只是个上网本，看看电影娱乐啥的，那肯定不用劳神了，不过如果要用JAVA来开发，还是老老实实的安装Sun JDK。还好的是，在Ubuntu 9.04以后，Sun JDK 安装已经越来越简单了。</p>
<p>1. 安装JDK</p>
<pre class="brush:shell">sudo add-apt-repository ppa:sun-java-community-team/sun-java6
sudo apt-get update
sudo apt-get install sun-java6-jdk</pre>
<p>2. 可以在 /etc/jvm 查看默认的 JVM, 或者</p>
<pre class="brush:shell">update-java-alternatives -s java-6-sun</pre>
<p>3. 添加环境变量 在 /etc/enviroment 中添加环境变量 ：</p>
<pre class="brush:plain">PATH="/usr/lib/jvm/java-6-sun/bin:$PATH"
CLASSPATH="/usr/lib/jvm/java-6-sun/lib"
JAVA_HOME="/usr/lib/jvm/java-6-sun"</pre>
<p><strong>顺便提一下Ubuntu10.10 里面的环境配置文件</strong>：</p>
<p>（1）/etc/enviroment 是系统的环境变量。</p>
<p>（2）/etc/profile： 是所有用户的环境变量。当用户第一次登录时,该文件被执行. 并从/etc/profile.d目录的配置文件中搜集shell的设置。</p>
<p>（3）/etc/bashrc: 为每一个运行bash shell的用户执行此文件.当bash shell被打开时,该文件被读取。</p>
<p>（4）~/.bash_profile: 每个用户都可使用该文件输入专用于自己使用的shell信息,当用户登录时,该文件仅仅执行一次!默认情况下,他设置一些环境变量,执行用户的.bashrc文件。</p>
<p>（5）~/.bashrc: 该文件包含专用于你的bash shell的bash信息,当登录时以及每次打开新的shell时,该该文件被读取。</p>
<p>（6） ~/.bash_logout:当每次退出系统(退出bash shell)时,执行该文件. 另外,/etc/profile中设定的变量(全局)的可以作用于任何用户,而~/.bashrc等中设定的变量(局部)只能继承 /etc/profile中的变量,他们是"父子"关系。</p>
<p>（7）~/.bash_profile 是交互式、login 方式进入 bash 运行的~/.bashrc 是交互式 non-login 方式进入 bash 运行的通常二者设置大致相同，所以通常前者会调用后者。</p>
