---
layout: post
title: Ubuntu 10.10 开发环境配置 （一）虚拟机安装
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
<p> 目前的项目很适合使用Linux开发，但是因为对 Windows 上的软件还是有相当的需求，所以决定还是保留了Windows，采用安装虚拟机作为开发环境。</p>
<p> 这样使用Ubuntu的速度是一个问题，不过感觉还是相当的不错，能够把开发环境隔离出来。相对于使用Windows 的 Desktop Toys Tool 来模拟多桌面，这个彻底的隔离来的更靠谱一些，而且很容易保留开发环境，只需要Pssuspend虚拟机就可以了。</p>
<p> 当然前提是电脑的配置还是要比较好的配置，目前我的电脑配置是双核，4G内存，足够满足要求了。</p>
<p>这次心情好，大概记录一下开发环境配置过程，以备以后使用吧。</p>
<p>关于虚拟机，种类也是相当多的，什么Vmware, VPC, Virtual Box, PCWare ... ok ，我只对Vmware 熟悉一点。 </p>
<p>你可以安装 VMware Workstation 目前的版本呢是7 ,VMware本身的安装还是极其简单，没什么好的，给个别人的链接看看就行了： VMware workstation 7 安装图解  </p>
<p>我安装的是 VMware server. VMware server从2.0版本才开始使用web管理界面,VI Web Access的好处就是让你能够通过浏览器从其他地方对虚拟机进行配置和管理，在浏览器中输入 https://VMwareserver:8333 启动VMware server管理界面.</p>
<p>图什么的就免了，总的来说还是很简单的东西。</p>
