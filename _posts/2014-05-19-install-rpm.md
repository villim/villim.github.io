---
layout: post
title: Install RPM
---

## Linux 

We have talked about install Oracle in 10.1o long time ago : Ubuntu 10.10 开发环境配置 （五）Install Database 

After these years, there's some change. First, Oracle changed the download website structure, you have to go <a title="Oracle Instant Client Downloads" href="http://www.oracle.com/technetwork/database/features/instant-client/index-097480.html" target="_blank">HERE </a>now. 

And Oracle didn't provide installer for non-rpm environment. I don't want to configure these stuff by my self. So in Ubuntu you can use **ALIEN** to install RPM packages.

<span style="color: #008000;"> alien is a program that converts between Red Hat rpm, Debian deb, Stampede slp, Slackware tgz, and Solaris pkg file formats. If you want to use a package from another linux distribution than the one you have installed on your system, you can use alien to convert it to your preferred package format and install it. It also supports LSB packages. </span>

**First, you have to install alien**
```bash	
	sudo apt-get install alien
```

**Then just install the RPM like**
```bash

	sudo alien -i oracle-instantclient-basic-10.2.0.5-1.i386.rpm
```

That's really easy and  wonderful ~
Infact, using "-i" alien first convert .rpm to .deb file. You can do it manually by
```bash

	sudo alien -k oracle-instantclient-basic-10.2.0.5-1.i386.rpm
```

**and then install deb file:**
```bash

	sudo dpkg -i oracle-instantclient-basic_10.2.0.5-1_i386.deb
```

## MacOS

```
brew install rpm
```

When using in Eclipse may encounter error, caused by incorrect link, fix with:

```
sudo ln -s /usr/local/Cellar/rpm/4.14.0/bin/rpmbuild /usr/bin/rpmbuild
```

