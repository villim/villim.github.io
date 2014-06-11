---
layout: post
title: Threadsafe Singleton
categories:
- JAVA
tags:
- Java
- Pattern
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
<p>单列模式是几乎成为了所有模式的入门课程。因为它又“简单”，又“复杂”。作为引入模式这个概念来说确实是不错的。不过经典 Singleton 在多线程时，并不是那么可靠，那么如何保证单例模式的线程安全呢？</p>
<p>Singleton，单例，顾名思义，是只存在一个的意思。程序里为了保证一致性，我们需要所有的操作都是一个唯一的对象来做。</p>
<h2><span style="color: #008000;">1. 先来看看经典单列</span></h2>
<p>它们的的特点是:</p>
<p>(1) static 的实例变量</p>
<p>(2) private 的构造函数</p>
<p>(3) 使用 getInstance() 返回对象</p>
<h3><span style="color: #993300;">1.1 Eager initialization singleton:</span></h3>
<pre class="brush:java">class EagerSingleton {
private static EagerSingleton instance = new EagerSingleton();

private EagerSingleton() { }

public static EagerSingleton getInstance() {
  return instance;
 }
}</pre>
<p>Eager initialization singleton 的 instance 在类初始化时initialized，并且 static 保证了 instance 只被初始化一次。单例模式是线程安全的。它只有一个被诟病的，就是 instance 初始化太早了。因为直到调用 getInstance() 方法之前，都是不需要 instance 的。</p>
<h3><span style="color: #993300;">1.2 lazy initialization singleton:</span></h3>
<pre class="brush:java">class LazySingleton {
private static LazySingleton instance;

private LazySingleton() { }

public static LazySingleton getInstance() {
if (instance == null) instance = new LazySingleton();
    return instance;
  }
}</pre>
<p>Lazy initialization singleton 唯一的不同是将初始化推迟到了 getInstance() 调用的时候。效率上来说，当然更好，不过有一个严重的问题，就是多线程时不再安全。如果两个线程同时进入 if(instance == null) 那么他们会生成两个对象。</p>
<h2><span style="color: #008000;">2. Initialization on demand holder idiom</span></h2>
<pre class="brush:java">public class Singleton {

private Singleton() { }

private static class SingletonHolder {
  public static final Singleton INSTANCE = new Singleton();
}

public static Singleton getInstance() {
    return SingletonHolder.INSTANCE;
  }
}</pre>
<p>这是一个比较新的单例实现方式，属于 Eager initialization singleton 的变种。实例对象 INSTANCE 仅当 getInstance() 调用的时候才会被初始化。 而静态类 SingletonHolder 在实例化时，由JVM保证了仅被初始化一次。 没有使用 volatile 和 synchronized。是相当简洁又有效的最佳实践，推荐使用。</p>
<h2><span style="color: #008000;">3. Double-checked locking</span></h2>
<p>Double-Check 是 Lazy initialization singleton 的变种。 我们一步步来看看经典的 Double-Check 是如何实现的。</p>
<p>首先直接加上 synchronized 的关键字 ：</p>
<pre class="brush:java">public static synchronized Singleton getInstance(){
  if (instance == null) instance = new Singleton();
  return instance;
}</pre>
<p>这是正确的写法，它能够保证线程安全。但是效率不高。因为每一次调用 getInstance() 方法都用 synchronized 做了同步块操作。 而其实我们只想在 instance 第一次被初始化的时候做 lock 而已。所以需要改进。</p>
<p>现在我们仅当 instance == null 的时候初始化</p>
<pre class="brush:java">public static Singleton getInstance() {
 if (instance == null) {
  synchronized(Singleton.class) {
  instance = new Singleton();
    }
  }
 return instance;
}</pre>
<p>问题是如果 thread1和thread2同事进入 if (instance == null ) 那么还是会分别实现自己的实例。Ok，现在终于到了经典的 Double-Checked Locking了：</p>
<pre class="brush:java">public static Singleton getInstance() {
  if (instance == null) { // 1
    synchronized(Singleton.class) {
      if (instance == null) // 2
        instance = new Singleton();
    }
  }
  return instance;
}</pre>
<p>看起来一切都符合逻辑了！！ 可惜 不是 .... 因为JVM的实现各有不同，有时会出现 “Out-of-order writes ”</p>
<p><span style="color: #993300;"><em><strong>Out-of-order writes Problem</strong></em>：</span></p>
<pre class="brush:plain">mem = allocate(); //Allocate memory for Singleton object.
instance = mem; //Note that instance is now non-null, but has not been initialized.
ctorSingleton(instance); //Invoke constructor for Singleton passing instance.</pre>
<p><em>即是说，thread1 和 thread 2 同时进入 //1 . 然后thread1先进入 //2 的位置，然后开始初始化，但是初始化还没有完成。 这时 thread2 发现 instance 不为null （thread1还没有完成的初始化） 就直接返回了。</em></p>
<p>关于这种情况，有人建议是 使用 volatile (variables declared volatile are supposed to be sequentially consistent, and therefore, not reordered)：</p>
<pre class="brush:java">public static volatile instance = null;</pre>
<p>但是 volatile 的问题是，许多 JVM 并没有按照 sequential consistency 正确的实现 volatile . 所以即便使用了 也可能失效</p>
<p>本文参考资料：</p>
<p><a href="http://www.ibm.com/developerworks/java/library/j-thread.html" target="_blank">http://www.ibm.com/developerworks/java/library/j-thread.html</a></p>
<p><a href="http://en.wikipedia.org/wiki/Singleton_pattern" target="_blank">http://en.wikipedia.org/wiki/Singleton_pattern</a></p>
<p><a href="http://www.ibm.com/developerworks/java/library/j-dcl.html" target="_blank">http://www.ibm.com/developerworks/java/library/j-dcl.html</a></p>
<p>&nbsp;</p>
