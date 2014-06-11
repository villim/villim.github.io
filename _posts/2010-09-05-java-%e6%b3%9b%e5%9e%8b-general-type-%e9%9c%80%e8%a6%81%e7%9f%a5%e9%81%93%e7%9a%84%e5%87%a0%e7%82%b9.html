---
layout: post
title: Java 泛型 (General Type) 需要知道的几点
categories:
- JAVA
tags:
- Generic
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
<p class="fswww1">什么是泛型（Generic Type）？</p>
<div>
<p>泛型的本质是参数化类型，也就是说所操作的数据类型被指定为一个参数。这种参数类型可以用在类、接口和方法的创建中，分别称为泛型类、泛型接口、泛型方法。</p>
<p>Java 在 J2SE 1.5 版本添加了对泛型的支持。为什么需要泛型呢？在JAVA中，总是不可避免的需要 downcast ，但是每个 downcast 对于<code>ClassCastException</code> 而言都是潜在的危险，应当尽量避免它们。而 J2SE 1.5之前即便再优良的设计也不可避免。例如：</p>
<p><span style="font-family: monospace;"><span style="line-height: normal; white-space: pre-wrap;"> </span></span></p>
<div id="_mcePaste"><span style="font-family: monospace;">class Hashtable {</span></div>
<div id="_mcePaste"><span style="font-family: monospace;">Object put(Object key, Object value) {...}</span></div>
<div id="_mcePaste"><span style="font-family: monospace;">Object get(Object key) {...}</span></div>
<div id="_mcePaste"><span style="font-family: monospace;">...</span></div>
<div id="_mcePaste"><span style="font-family: monospace;">}</span></div>
<div id="_mcePaste"><span style="font-family: monospace;">class Test {</span></div>
<div id="_mcePaste"><span style="font-family: monospace;">public static void main(String[] args) {</span></div>
<div id="_mcePaste"><span style="font-family: monospace;">Hashtable h = new Hashtable();</span></div>
<div id="_mcePaste"><span style="font-family: monospace;">h.put(new Integer(0), "value");</span></div>
<div id="_mcePaste"><span style="font-family: monospace;">String s = (String)h.get(new Integer(0));</span></div>
<div id="_mcePaste"><span style="font-family: monospace;">System.out.println(s);</span></div>
<div id="_mcePaste"><span style="font-family: monospace;">}</span></div>
<div id="_mcePaste"><span style="font-family: monospace;">}</span></div>
<p><span style="font-family: monospace;">class Hashtable {  Object put(Object key, Object value) {...}  Object get(Object key) {...}  ...}class Test {  public static void main(String[] args) {    Hashtable h = new Hashtable();    h.put(new Integer(0), "value");    String s = (String)h.get(new Integer(0));    System.out.println(s);  }}</span></p>
<p>如果使用泛型，我们可以这么解决问题:</p>
<p><span style="font-family: monospace;"><span style="line-height: normal; white-space: pre-wrap;">class Hashtable&lt;Key, Value&gt; {</span></span></p>
<p><span style="font-family: monospace;"><span style="line-height: normal; white-space: pre-wrap;"> ...</span></span></p>
<p><span style="font-family: monospace;"><span style="line-height: normal; white-space: pre-wrap;"> Value put(Key k, Value v) {...}</span></span></p>
<p><span style="font-family: monospace;"><span style="line-height: normal; white-space: pre-wrap;"> Value get(Key k) {...}</span></span></p>
<p><span style="font-family: monospace;"><span style="line-height: normal; white-space: pre-wrap;">}</span></span></p>
<p><span style="font-family: monospace;"><span style="line-height: normal; white-space: pre-wrap;">class Test {</span></span></p>
<p><span style="font-family: monospace;"><span style="line-height: normal; white-space: pre-wrap;"> public static void main(String[] args) {</span></span></p>
<p><span style="font-family: monospace;"><span style="line-height: normal; white-space: pre-wrap;"> Hashtable&lt;Integer, String&gt; h = new Hashtable&lt;Integer, String&gt;();</span></span></p>
<p><span style="font-family: monospace;"><span style="line-height: normal; white-space: pre-wrap;"> h.put(new Integer(0), "value");</span></span></p>
<p><span style="font-family: monospace;"><span style="line-height: normal; white-space: pre-wrap;"> ...</span></span></p>
<p><span style="font-family: monospace;"><span style="line-height: normal; white-space: pre-wrap;"> }</span></span></p>
<p><span style="font-family: monospace;"><span style="line-height: normal; white-space: pre-wrap;">}</span></span></p>
<p>略过泛型的具体使用介绍，我们来看看几件必须知道的事情：</p>
<p>1. 必须用引用类型进行实例化,基本类型不起作用。<br />
因此，在上面示例中，无法完成创建从 int 映射到 String 的 Hashtable 。</p>
<p>2.泛型不支持类继承</p>
<p><span style="font-family: monospace;"><span style="line-height: normal; white-space: pre-wrap;">List&lt;Number&gt; numbers = new ArrayList&lt;Integer&gt;(); // will not compile</span></span></p>
<p><span style="font-family: monospace;"><span style="line-height: normal; white-space: pre-wrap;">List&lt;Long&gt; list = new ArrayList&lt;Long&gt;();</span></span></p>
<p><span style="font-family: monospace;"><span style="line-height: normal; white-space: pre-wrap;">List&lt;Number&gt; numbers = list; // this will not compile</span></span></p>
<p>3.在JAVA中，泛型的实现是擦除法。</p>
<p>编译器在生成类文件时基本上会抛开参数化类的大量类型信息。也就是说编译器会将泛型类型以其父类代替，如String变成了Object等。<br />
尽管不能将 List&lt;Integer&gt; 赋给 List&lt;Number&gt;，但是</p>
<p><span style="font-family: monospace;"><span style="line-height: normal; white-space: pre-wrap;"> new List&lt;Number&gt;().getClass() == new List&lt;Integer&gt;().getClass() </span></span></p>
<p>4.不能创建泛型数组</p>
<p>T[] arr = new T[10];// this code will not compile</p>
<p>List&lt;Integer&gt;[] array = new List&lt;Integer&gt;[10]; // does not compile</p>
<p>因为数组本身是支持类继承的:</p>
<p>Number[] a = new Number[10];</p>
<p>a[1] = Integer.valueOf(1);</p>
<p>4.不能创建泛型数组<br />
<span style="font-family: monospace;"><span style="line-height: normal; white-space: pre-wrap;">T[] arr = new T[10];// this code will not compile</span></span></p>
<p><span style="font-family: monospace;"><span style="line-height: normal; white-space: pre-wrap;">List&lt;Integer&gt;[] array = new List&lt;Integer&gt;[10]; // does not compile</span></span></p>
<p>因为数组本身是支持类继承的。</p>
<p><span style="font-family: monospace;"><span style="line-height: normal; white-space: pre-wrap;">Number[] a = new Number[10]; a[1] = Integer.valueOf(1);</span></span></p>
<p>5.使用通配符<br />
5.1 &lt;? extends E&gt;</p>
<p>java.util.List.java</p>
<p>boolean addAll(Collection&lt;? extends E&gt; c);</p>
<p>List&lt;? extends Long&gt; list = new ArrayList();</p>
<p>List&lt;Long&gt; longlist = new ArrayList();</p>
<p>list = longlist;<br />
5.2 &lt;? super E&gt;</p>
<p>List&lt;? super Long&gt; list = new ArrayList();</p>
<p>List&lt;Number&gt; longlist = new ArrayList();</p>
<p>list = longlist;</p>
<p>6. Multiple Bounds</p>
<p>例如你定义约束是这个类必须是Number，并且应该继承i</p>
<p>public static &lt;T extends Number &amp; Comparable&lt;? super T&gt;&gt; int compareNumbers(T t1, T t2){</p>
<p>return t1.compareTo(t2);</p>
<p>}</p>
<p>public static &lt;T extends String &amp; Number &gt; int compareNumbers(T t1, T t2) // does not work..can't have two classes</p>
<p>public static &lt;T extends Comparable&lt;? super T&gt; &amp; Number &gt; int compareNumbers(T t1, T t2) // does not work..</p>
<p>public static &lt;T extends CharSequence &amp; Comparable&lt;T&gt;&gt; int compareNumbers(T t1, T t2)// works..multiple interfaces</p>
</div>
