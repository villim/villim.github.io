---
layout: post
title: 用Vim开发 ： 格式化代码
categories:
- LINUX
- OTHER
tags:
- Vim
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
<p>想用 Vim 开发，第一个问题就是：如何格式化代码？之前关于 <a title="VIM Configuration for C" href="http://www.from0to1.net/vim-configuration-for-c/">Vim 配置</a> 里已经有关于 Tab 的控制，如何进行自动缩进。可是当然免不了要自己动手的时候。</p>
<p>本来以为还需要插件才能把这事儿给办了，不过还是不了解Vim大哥，其实做起来相当方便快捷。</p>
<p>首先要知道的是，<span style="color: #008000;"><strong>全文格式化</strong></span>：</p>
<pre class="brush:shell">gg=G</pre>
<p>命令很简单，只要知道 “ <strong>=</strong> ” 是格式化对齐代码，就不难记得如何做了。</p>
<p>选择指定的一些代码来格式化，也是必须的，最为直观好用的，是<span style="color: #008000;"><strong>可视化的选择一些行来格式化</strong></span>：</p>
<pre class="brush:shell">v [jk] =</pre>
<p>当然如果只有一行代码，没有必要做任何选着，可以简单的 <span style="color: #008000;"><strong>格式化当前行</strong></span>：</p>
<pre class="brush:shell">==</pre>
<p>代码行里的  “{” 和 “}” 也能给我们 <span style="color: #008000;"><strong>格式化方法</strong></span> 带来很大的帮助：</p>
<pre class="brush:shell">=}   //从当前行格式化到}
={   //从当前行格式化到{</pre>
<p>但是要特别注意，当你的代码在{}里有多个代码块的时候，却并不能这样格式化所有的内容，比如有下面的代码：</p>
<pre class="brush:java">    protected Session getImapSession() {
        Properties props = new Properties(); // 代码块1
        props.put("mail.imaps.host", getHostname());

        return Session.getInstance(props); // 代码块2
    }</pre>
<p>因为空行，这个方法有2个代码块，这个时候 “ =}” 或者 “={” 并不能格式化所有的东西。这个时候你需要指定<span style="color: #008000;"><strong>格式化代码块</strong></span>：</p>
<pre class="brush:shell">=i}   //从当前行格式化到}
=i{   //从当前行格式化到{</pre>
