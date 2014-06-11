---
layout: post
title: Boxing Conversion 里的灵异事件
categories:
- JAVA
tags:
- Boxing
- Java
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
<p>Java 的 Boxing 是一个很基本的东西，一开始学习 Java 的数据类型就能接触到。比如， boolean 的 wrapper:Boolean; byte 的 wrapper:Byte ... ... 但凡看过Java介绍的估计没有人不知道。J2SE5开始又加入了自动包装的概念 （AutoBoxing），有些东西就变得诡异起来了。来看看下面这段代码，你能正确说出结果吗？</p>
<pre class="brush:java">		int integer = 127;
		Integer obj1 = integer;
		Integer obj2 = integer;
		System.out.println(obj1 == obj2);

		integer = 128;
		Integer obj3 = integer;
		Integer obj4 = integer;
		System.out.println(obj3 == obj4);</pre>
<p>==================请先自己思考一下==================</p>
<p>结果是否出乎意料？ 第一个输出是 True；第二个输出是 False。仅仅从127变成128,怎么会有这样的区别？</p>
<p>原因可以从 <a title="Java Language Specification 3rd Ed" href="http://java.sun.com/docs/books/jls/third_edition/html/j3TOC.html" target="_blank"><strong><em>The Java Language Specification, Third Edition </em></strong></a>中找到：</p>
<p>下面几种情况将 Primitive type 转化为包装类，以下几种情况是我们所谓的 <strong>Boxing Conversion</strong>:</p>
<ul>
<li>From type <code>boolean</code> to type <code>Boolean</code> <a name="202793"></a></li>
<li>From type <code>byte</code> to type <code>Byte</code> <a name="202794"></a></li>
<li>From type <code>char</code> to type <code>Character</code> <a name="202795"></a></li>
<li>From type <code>short</code> to type <code>Short</code> <a name="202796"></a></li>
<li>From type <code>int</code> to type <code>Integer</code> <a name="202797"></a></li>
<li>From type <code>long</code> to type <code>Long</code> <a name="202798"></a></li>
<li>From type <code>float</code> to type <code>Float</code> <a name="202799"></a></li>
<li>From type <code>double</code> to type <code>Double</code></li>
</ul>
<p><span style="color: #800000;"><em><strong>If the value p being boxed is <code>true</code>, <code>false</code>, a <code>byte</code>, a <code>char</code> in the range \u0000 to \u007f, or an <code>int</code> or <code>short</code> number between -128 and 127, then let r1 and r2 be the results of any two boxing conversions of p. It is always the case that r1 == r2.</strong></em></span></p>
<p>显然即是说，Java 将较小的这段值，Cache了起来，用来重用。这应该是为某些有内存限制的环境，能够节省开销的策略。虽然有些诡异，但是都是些 Primitive 类型，其实基本不可能会影响到实际的使用。</p>
