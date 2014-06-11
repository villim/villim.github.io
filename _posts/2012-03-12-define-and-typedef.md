---
layout: post
title: C语言学习：#define 与 typedef
categories:
- C/C++
tags:
- C
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
<p><strong>在</strong>C语<strong>言里，<span style="color: #000000;">#define</span></strong> 与 <span style="color: #000000;"><strong>typedef</strong></span> 看起来是挺接近的东西。我们可以让他们达到相同的效果，比如：</p>
<pre class="brush:cpp">#define MY_TYPE int
typedef int My_Type;</pre>
<p>但本质来说，他们的区别可大了去了。</p>
<h5><strong><span style="color: #993300;">1. 编译时间不同</span></strong></h5>
<ul>
<li><span style="color: #000000;"><strong><code>#define</code></strong></span> <em>is a preprocessor token: the compiler itself will never see it.</em></li>
</ul>
<ul>
<li><span style="color: #000000;"><strong><code>typedef</code></strong></span> <em>is a compiler token: the preprocessor does not care about it.</em></li>
</ul>
<p>#define是在预编译阶段编译的，而typedef是在编译的时候才执行的。</p>
<p><span style="color: #993300;"><strong>2. #define只是简单的替换，而typedef是为一个原有的关键字起一个“别名”。</strong></span></p>
<h6><span style="color: #008000;">2.1 #define 经常被用来处理“魔数”问题</span>，例如</h6>
<pre class="brush:cpp">#define PI 3.1415926;</pre>
<h6><span style="color: #008000;">2.1 typedef的主要用在给结构体起别名</span>，例如：</h6>
<h6 class="brush:cpp">typedef struct student<br />
{<br />
char name[16];<br />
int age;<br />
double score;<br />
} Stu,*pStu;</p>
<p><span style="color: #008000;">2.3 定义指针时的区别</span></h6>
<pre class="brush:cpp">typedef int* int_p1;
int_p1 a, b, c;  // a, b, and c are all int pointers.

#define int_p2 int*
int_p2 a, b, c;  // only the first is a pointer!</pre>
<h6>
<span style="color: #008000;">2.4 只能用 typedef 的时候</span></h6>
<pre class="brush:cpp">#define MY_TYPE void (*)(int)
typedef void (*fun_p)(int);

void fx_typ(fun_p fx); /* ok */
void fx_def(MY_TYPE fx); /* error */

typedef int arr[10];
arr a, b, c; // create three 10-int array</pre>
<h5></h5>
<h5><span style="color: #993300;">3.参数问题：#define是可以带参数的</span>，例如：</h5>
<pre class="brush:cpp">#define XX(a,b) myfun(a,b);</pre>
