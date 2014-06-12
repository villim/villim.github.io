---
layout: post
title: Install RPM on Ubuntu
categories:
- LINUX
tags:
- alien
- Oracle
- rpm

---

<p>We have talked about install Oracle in 10.1o long time ago :
 {% post_link 2010-10-26-ubuntu-10-10-5-install-database Ubuntu 10.10 install Database %}
 
<p>After these years, there's some change. First, Oracle changed the download website structure, you have to go <a title="Oracle Instant Client Downloads" href="http://www.oracle.com/technetwork/database/features/instant-client/index-097480.html" target="_blank">HERE </a>now. 

And Oracle didn't provide installer for non-rpm environment. I don't want to configure these stuff by my self. So in Ubuntu you can use **ALIEN** to install RPM packages.

<p><span style="color: #008000;"> alien is a program that converts between Red Hat rpm, Debian deb, Stampede slp, Slackware tgz, and Solaris pkg file formats. If you want to use a package from another linux distribution than the one you have installed on your system, you can use alien to convert it to your preferred package format and install it. It also supports LSB packages. </span><p>

**First, you have to install alien**
{% highlight bash %}	
	sudo apt-get install alien
{% endhighlight %}

**Then just install the RPM like**
{% highlight bash %}

	sudo alien -i oracle-instantclient-basic-10.2.0.5-1.i386.rpm
{% endhighlight %}

That's really easy and  wonderful ~
Infact, using "-i" alien first convert .rpm to .deb file. You can do it manually by
{% highlight bash %}

	sudo alien -k oracle-instantclient-basic-10.2.0.5-1.i386.rpm
{% endhighlight %}

**and then install deb file:**
{% highlight bash %}

	sudo dpkg -i oracle-instantclient-basic_10.2.0.5-1_i386.deb
{% endhighlight %}
