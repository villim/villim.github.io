---
layout: post
title: How do I use Grep
categories:
- LINUX
tags:
- Grep
status: publish
type: post
published: true
meta:
  _wp_old_slug: ''
author:
  login: villim
  email: villim@126.com
  display_name: Villim
  first_name: Villim
  last_name: Wong
---
<p>如果要使用Linux来做软件开发，不使用Grep基本就是自废武功，用好了自然也能事半功倍。<br />
重要性当然是极其明了，不过我现在也只是入门而已，还谈不上什么奇技淫巧，大概记录一下目前的使用方法。</p>
<h2><span style="color: #008000;">1. 在单个文件中查找</span></h2>
<pre class="brush:shell">grep sometext  ~/Desktop/Test.txt</pre>
<p>最基本的基本使用，注意的是能够匹配 "abcsometext" 和 "sometextabc"。</p>
<pre class="brush:shell">grep ^sometext ~/Desktop/Test.txt</pre>
<p>查找以 “sometext” 开头的内容。</p>
<pre class="brush:shell">grep -w sometext ~/Desktop/Test.txt</pre>
<p>查找 单词 “sometext”</p>
<pre class="brush:shell">grep '<pre wp-pre-tag-3></pre>lt;s...t..t<pre wp-pre-tag-3></pre>gt;'  ~/Desktop/Test.txt</pre>
<p>使用正则表达式匹配单词</p>
<p>还有几个常用参数：<br />
<strong>-i</strong> 忽略大小写<br />
<strong>-v</strong> 查询不匹配给定的参数<br />
<strong>-l </strong>只列出匹配的文件名<br />
<strong>-c</strong> 统计匹配到的总数</p>
<h2><span style="color: #008000;">2. 递归查询</span></h2>
<pre class="brush:shell">grep -rl sometext ~/Desktop</pre>
<h2><span style="color: #008000;">3. 配合Find提高效率</span></h2>
<pre class="brush:shell"> find  ~/Desktop/ -name *.txt -exec grep -lw 'sometext' {} +</pre>
<h2><span style="color: #008000;">4. 查询多个参数</span></h2>
<pre class="brush:shell">egrep -w 'testa | testb' ~/Desktop</pre>
