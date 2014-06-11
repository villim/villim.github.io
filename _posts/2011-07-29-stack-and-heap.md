---
layout: post
title: Stack and Heap
categories:
- C/C++
- JAVA
tags:
- C
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
<p>通常都看到书籍文章中，Stack 的中文翻译一会儿说是”堆栈“。一会儿又有人说”堆“是堆，”栈“是栈 ...<br />
把简单的东西弄得绕来绕去，头也会大。所以还是直接用英文更准确一些。Java 和 C 关于它们的概念都是相通的。</p>
<p><span style="color: #008000;">Stack有两个概念。</span></p>
<p>首先它是一种 <a href="http://en.wikipedia.org/wiki/Stack_(data_structure)" target="_blank">Abstract Data Type</a>。 就是常说的 Last In First Out 数据模型。但是当把 Stack 和 Heap 放在一起的时候，我们通常指的是另外一个概念，指的是 <a href="http://en.wikipedia.org/wiki/Stack_(data_structure)#Hardware_stacks" target="_blank">Hardware Stacks</a> ，是对 memory 的分配和使用方式。<br />
在 Java 中的 memory 的使用，通常有以下几种：</p>
<ol>
<li><em><strong><span style="color: #993300;"> Register</span>：</strong>我们在程序中无法控制</em></li>
<li><em><strong><span style="color: #993300;">Stack</span> ：</strong>存放基本类型的数据和对象的引用，但对象本身不存放在栈中，而是存放在堆中</em></li>
<li><em><strong><span style="color: #993300;">Heap</span> ：</strong>存放用new产生的数据。（Java和C对Heap处理不同，Java由垃圾收集器自动管理）</em></li>
<li><em><strong><span style="color: #993300;">Static Field</span> ：</strong>存放在对象中用static定义的静态成员</em></li>
<li><em><strong><span style="color: #993300;">Constant Pool</span>：</strong>存放常量</em></li>
<li><em><strong><span style="color: #993300;">Non-RAM</span> ： </strong>(随机存取存储器)存储：硬盘等永久存储空间</em></li>
</ol>
<p>Stack 是从高地址往下分配。 只有 push 和 pop 两个操作，可能会碰到的问题是，当指针指向低于最小值的时候，a stack underflow occurs. 反之，如果大于乐最大地址值，a stack overflow occurs.  它的优点是速度快，有数据共享的功能。它是在对象实例化的时候分配的空间，通过 new 创建； java中不需要显示释放，由垃圾收集器自动管理。</p>
<p>直接看例子最容易理解：<br />
对于String这个类来说，可由两个方式建立：</p>
<pre class="brush:shell">String s = new String ("ABC");</pre>
<p><span class="Apple-style-span" style="font-family: Georgia, 'Times New Roman', 'Bitstream Charter', Times, serif; font-size: 13px; line-height: 19px; white-space: normal;"> “s” 在Stack里，而但"ABC" 在 Heap 中会不断地创建新的对象 </span></p>
<pre class="brush:shell">String s = "ABC";
String b = "A" + "BC";</pre>
<p><span class="Apple-style-span" style="font-family: Georgia, 'Times New Roman', 'Bitstream Charter', Times, serif; font-size: 13px; line-height: 19px; white-space: normal;">"S" 和 "b"  都在 Stack 中。“ABC” ， “A” 和 “BC” 在 Constant Pool 中。然后 JVM 会把它们优化到同一个 “ABC” 。所以 S 和 B 指向同一个位置。</span></p>
<p><span style="color: #008000;">在 JAVA 的 JVM 中，通常把 Memory 的概念简化为：</span></p>
<p>1. <strong>Heap Memory</strong></p>
<pre class="brush:plain">-Xmx&lt;size&gt; - to set the maximum Java heap size
-Xms&lt;size&gt; - to set the initial Java heap size</pre>
<p>2. <strong>Non Heap Memory</strong></p>
<pre class="brush:plain">-XX:MaxPermSize=128m</pre>
<p>3. <strong>Other</strong></p>
<p><span style="color: #008000;">再来看一个C的例子：</span></p>
<pre class="brush:cpp">//main.cpp
int a = 0; 全局初始化区
char *p1; 全局未初始化区
main()
{
int b; 栈
char s[] = "abc"; 栈
char *p2; 栈
char *p3 = "123456"; 123456<pre wp-pre-tag-4></pre>在常量区，p3在栈上。
static int c =0； 全局（静态）初始化区
p1 = (char *)malloc(10);
p2 = (char *)malloc(20);
分配得来得10和20字节的区域就在堆区。
strcpy(p1, "123456"); 123456<pre wp-pre-tag-4></pre>放在常量区，编译器可能会将它与p3所指向的"123456"优化成一个地方。
}</pre>
