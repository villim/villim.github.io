---
layout: post
title: Ubuntu 10.10 开发环境配置 （二）Install Ubuntu
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
<h3>1. 安装 Virtual Machine</h3>
<p>1.1 通过VMware Infrastructure Web Access登陆vmware</p>
<p>1.2 选择Virtual Machines -&gt; Create Virtual Machine. </p>
<p>1.2.1 给虚拟机取个名字，选择虚拟机文件存放位置</p>
<p>1.2.2 接下来选择 Linux Operation System </p>
<p>1.2.3 分配虚拟机使用的内存大小，我分配 1.5G</p>
<p>1.2.4 配置虚拟机磁盘大小及存储路径，我分配了30G物理硬盘</p>
<p>1.2.5 接下来一路Next ，详细可以参考 <a href="http://www.linuxidc.com/Linux/2010-06/26801.htm" target="_blank">这里</a> </p>
<p>1.3  Unbuntu10.10 的安装 ，详细参见 : <a href="http://www.cnblogs.com/zxppc/archive/2010/10/11/1847816.html" target="_blank">Ubuntu 10.10 Netbook 安装图解</a></p>
<p>这里只需要说一下在 “分配磁盘空间” : </p>
<p>建议分配3G左右的SWAP空间； 再分100M专门挂载 /boot </p>
<h3>2. Install VMware Tool</h3>
<p>安装VMware可以改变虚拟机显示的大小，也可以让真机喝虚拟机实现字符串相互拷贝,相互分享共享目录......</p>
<p>2.1 通过VMware Infrastructure Web Access登陆vmware</p>
<p>2.2 点击虚拟机上的安装vmware tools，回到虚拟机(Ubuntu)桌面回看到一个vmware tools的cdrom图标。</p>
<p>2.3 打开它，复制“vmwaretools....tar.gz”，到 /home/{user} ; 解压为文件夹 vmwaretools....</p>
<p>2.4 查看vmwaretools下的.pl文件是否有执行权限，如果没有则添加</p>
<p>2.5 sudo ./vmware-install.pl</p>
<p>2.6 接下来一路输入YES，直到你看到---the vmware team就可关闭窗口，然后重新启</p>
<p>也可以参考 <a href="http://edu.kafan.cn/html/xuniji/vmware/11272.html">这里</a></p>
<h3>Ubuntu 10.10 在安装的时候目前会碰到几个问题：</h3>
<pre class="brush:plain">What is the location of the directory of C header files that match your running

kernel? [/usr/src/linux/include] &lt;直接按 Enter&gt;


The path "/usr/src/linux/include" is not an existing directory.</pre>
<p> </p>
<p>由于 Kernel 版本是 APT 抓下來的最新版，所以会需要输入 “/usr/src/linux-headers-2.6.35-22-generic/include “ </p>
<p>要注意的是，VMWare Tools 安装时会询问目前系统使用的 Kernel header，所以如果 /usr/src 下有多个 Kernel header 目录，最好先执行 “uname -r“ 指令，确认应该使用那个本版。另外可以不直接使用 “/usr/src/linux-headers-2.6.35-22-generic/include” ，先 “<strong>sudo ln -s  /usr/src/linux-headers-2.6.35-22-generic  /usr/src/linux</strong>”</p>
<pre class="brush:plain">What is the location of the directory of C header files that match your running

kernel? [/usr/src/linux/include] /usr/src/linux-headers-2.6.35-22-generic/include</pre>
<p>按回车以后，还是报错说，指定的Kernel headers喝当前系统使用的版本不匹配。</p>
<pre class="brush:plain">The directory of kernel headers (version @@VMWARE@@ UTS_RELEASE) does not match

your running kernel (version 2.6.35-22-generic). Even if the module were to

compile successfully, it would not load into the running kernel.</pre>
<p>但事实并不是不匹配，而是 Kernel 中有一个变量 UTS_RELEASE 的不存在了。以前这个定义放在 /usr/src/linux-headers-2.6.35-22-generic/include/linux/version.h ，而现在已经移到了/usr/src/linux-headers-2.6.35-22-generic/include/linux/utsrelease.h。所以简单的方法，我们只需要在<strong>version.h</strong>中添加 <strong>#define UTS_RELEASE "2.6.35-22-generic"</strong> （具体值使用 “uname -r“ 查看）</p>
<p> 接下来继续，又会有新的错误提示!! -_-|| 找不到 autoconf.h 原因是因为 autoconf.h 不再VMware tools 安装程序预设的寻址目录中。</p>
<pre class="brush:plain">The path "/usr/src/linux-headers-2.6.35-22-generic/include" is a kernel header

file directory, but it does not contain the file "linux/autoconf.h" as

expected. This can happen if the kernel has never been built, or if you have

invoked the "make mrproper" command in your kernel directory. In any case, you

may want to rebuild your kernel.</pre>
<p>可以简单的把它链接过来：</p>
<pre class="brush:shell">cd /usr/src/linux-headers-2.6.35-22-generic/include/linux


sudo ln -s ../generated/autoconf.h ./</pre>
<p> </p>
<p>然后应该能顺利完成安装了。</p>
