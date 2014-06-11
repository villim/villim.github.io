---
layout: post
title: 再探 InvokeDynamic
categories:
- JAVA
tags:
- Invokevirtual
- Java
- Java7
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
<p>在之前，我们说到 <a title="What’s new in Java SE7" href="http://www.from0to1.net/what-is-new-in-java-se7/" target="_blank">What's new in Java SE7</a> 的时候。我们已经说到了 <span style="color: #333399;"><strong>invokedynamic</strong></span> 这个 Java 自诞生以来，首个新的字节码指令。不过关于它是如何运作的，说得还是相当模糊。需要再把整个链条理一理。主要参考了 <strong>Ed Ort</strong> 关于<a title="New JDK 7 Feature: Support for Dynamically Typed Languages in the Java Virtual Machine" href="http://java.sun.com/developer/technicalArticles/DynTypeLang/index.html" target="_blank">Java7 InvokeDynamic新特性</a>的文章。<strong></strong></p>
<h3><span style="color: #008000;"><strong>关于 JVM</strong></span></h3>
<p>我们都知道，JVM 执行Java程序，把Java代码转化成为 machine-independent 的 bytecode。其实 JVM 和 Java 编程语言是独立的。他依赖的是一种特殊的二进制格式代码，一种 <em>class</em> 文件格式。  所以其实，任何一种语言，只要它能表述成为合法的 <em>class</em> 格式文件，就能由 JVM 来执行。</p>
<h3><span style="color: #008000;"><strong>为什么动态语言要在 JVM 上运行？</strong></span></h3>
<p>动态语言的特点不用仔细描述了，简单的说由于大多数动态语言都是弱类型的，高度集成让语法简单，代码简介，能极大提高开发效率。但是，通常使用强类型的语言在执行的时候有更好地效率。使用强类型还可以在编译的时候消除大量错误。把两者的优点结合起来就是让 JVM 支持动态语言的最好动机了。</p>
<p>从 Java6 （JSR223）开始，JVM 已经努力在支持动态语言。Java6 中使用 Script Engine ，来编译和解释并执行脚本语言。目前已经有超过20种脚本语言Engine，能够轻松的在 JVM 里运行。</p>
<h3><span style="color: #008000;"><strong>JVM 是怎么工作的？</strong></span></h3>
<p>要在程序在 JVM 里面运行，毫无疑问，你必须遵循 JVM 的规则。直到现在，这个规则就是，bytecode 只能是强类的。强类型语言（Statically typed language）要求在编译的时候，检查return value 的类型和传入参数的类型。比如下面这段代码，</p>
<pre class="brush:java">   String s = "Hello World";
   System.out.println(s);</pre>
<p>println（）的参数必须是 String，而虽然没有明确的返回值，但其实它的返回类型是 java.io.PrintStream. 然后 Javac 会把它编译为这样的 bytecode 代码：</p>
<pre class="brush:java">   ldc #2  // Push the String "Hello World" onto the stack
   astore_1 // Pop the value "Hello World" from the stack and store it in local variable #1
   getstatic #3 // Get the static field java/lang/System.out:Ljava/io/PrintStream from the class
   aload_1 // Load the String referenced from local variable #1
   invokevirtual #4 // Method java/io/PrintStream.println:(Ljava/lang/String;)V</pre>
<p>很明显这里的 invokevirtual 和其他的stack操作不同，它调用了一个方法。</p>
<ul>
<li>The receiver class providing the method: <code>java.io.PrintStream</code></li>
<li>The method name: <code>println</code></li>
<li>The type of the method argument: <code>(Ljava/lang/String;)</code> for <code>String</code></li>
<li>The method's return type: <code>V</code> for <code>void</code></li>
</ul>
<p>这里提供的签名信息帮助JVM在类中找到正确的方法，如果找不到，它会继续到父类中寻找。</p>
<h3> <span style="color: #008000;"><strong>动态语言带来的问题？</strong></span></h3>
<p>动态语言的类型要到` runtime 才能被确定，来下面这个抽象的动态语言代码来说：</p>
<pre class="brush:scala">   function max (x,y) {
      if x.lessThan(y) then y else x
   }</pre>
<p>注意，参数和返回值都是没有了类型的，这违反了在编译时就需要直到类型的规则，所以这个代码是无法在Java平台里被成功编译的。那么我们如何解决这个问题呢？</p>
<p><span style="color: #993300;"><strong>1. 创建 Language-specific Java Types</strong></span></p>
<pre class="brush:java">   MyObject function max (MyObject x,MyObject y) {
      if x.lessThan(y) then y else x
   }</pre>
<p>这个 Language-specific 的基类 MyObject 必须包涵了 isLessThan 和其他一切动态语言可能用到的方法。问题显而易见，首先动态语言的设计者，必须一开始就给 MyObject设计好所有的方法。而且 JVM 几乎不能之用系统定义的类型，比如 String 和 Integer 等等。</p>
<p><span style="color: #993300;"><strong>2. 使用反射</strong></span></p>
<p>使用 java.lang.reflect.Method 对象来调用方法。在 Runtime的时候，根据类型调用类或者接口的方法。但可惜不是所有的动态语言都能提供Java的类型。</p>
<p><span style="color: #993300;"><strong>3. 实现一个 language-specific 解释器</strong></span></p>
<p>在 JVM 层之上实现一个自己的解释层，在方法调用的时候做处理。相对来说，这种方式比让 JVM直接处理会慢很多。</p>
<h3><span style="color: #008000;"><strong>InvokeDynamic 来了</strong></span></h3>
<p>毫无疑问，JSR292 中的 <strong>InvokeDynamic</strong> 就是来解决这个问题的。同时被引入的，还有一种新的方法关联机制。</p>
<p><span style="color: #993300;"><strong>我们先来看看之前的4个 invoke 方法：</strong></span></p>
<ul>
<li><strong><code>invokevirtual</code></strong> - Invokes a method on a class. This is the typical type of method invocation.</li>
<li><strong><code>invokeinterface</code></strong> - Invokes a method on an interface.</li>
<li><strong><code>invokestatic</code></strong> - Invokes a static method on a class. This is the only kind of invocation that lacks a receiver argument.</li>
<li><strong><code>invokespecial</code></strong> - Invokes a method without reference to the type of the receiver. Methods called this way can be constructors, superclass methods, or private methods.</li>
</ul>
<p>我们仔细看其中两个：<strong><code>invokevirtual （</code></strong><code>最典型的</code><strong><code>）</code></strong>和 <strong><code>invokeinterface （</code></strong><code>和 invokedynamic最接近</code><strong><code>）</code></strong></p>
<p><strong><span style="color: #993300;"><code>invokevirtual</code> 的定义是</span></strong>：</p>
<pre class="brush:java">invokevirtual &lt;method-specification&gt;</pre>
<p>再看看之前的例子：</p>
<pre class="brush:java">invokevirtual #4; //Method java/io/PrintStream.println:(Ljava/lang/String;)V</pre>
<p>我们可以看到 <code>invokevirtual的 &lt;method-specification&gt; 提供了方法名，参数和返回值的所有信息。</code></p>
<p><span style="color: #993300;"><strong><code>invokeinterface 的定义是</code></strong></span><code><span style="color: #993300;"><strong>：</strong></span><br />
</code></p>
<pre class="brush:java">invokeinterface &lt;method-specification&gt; &lt;n&gt;</pre>
<p>它的Bytecode看起来应该差不多是这样：</p>
<pre class="brush:java">invokeinterface #9,  2; //InterfaceMethod java/util/List.add:(Ljava/lang/Object;)Z</pre>
<p>这里的 <code>&lt;method-specification&gt; 提供了接口的名字，方法名，</code>参数和返回值。而 &lt;n&gt; 说明了参数的个数，包括返回值。</p>
<p><span style="color: #993300;"><strong><code>invokedynamic 的定义是：</code></strong></span></p>
<pre class="brush:java"> invokedynamic &lt;method-specification&gt; &lt;n&gt;</pre>
<p>它的bytecode看起来差不多是这样：</p>
<pre class="brush:java">Invokedynamic #10; //NameAndTypelessThan:(Ljava/lang/Object;Ljava/lang/Object;)</pre>
<p>很明显，和 invokeinterface不同的是，&lt;method-specification&gt; 只需要指名方法名字和参数就行了，而且并不需要申明 &lt;n&gt;.  这样做么没有乐返回类型, 使得动态语言在方法调用的时候，不需要指定目标类型是否包涵了这个方法，就可成功编译。</p>
<h3><span style="color: #008000;"><strong>新的动态链接机制：Method Handles</strong></span></h3>
<p>现在不需要指定目标类型了，那么 JVM怎么找到正确的方法来执行呢？</p>
<p>现在在 Java7 中增加了一个 java.lang.invoke.* 包，用来增加对动态语言的支持。其中 <code>java.lang.invoke.MethodHandle 包含了指向 JVM 中方法的引用。和之前通过名字来访问最大的区别就在于，它是通过 point structure来访问。</code></p>
<p>和其他的 invoke instructions 一样, 当 invokedynamic instruction 第一次被执行的时候, 它就被关联了. 当这个链接创建时, 一个 method handle 被指定给这个唯一的 invokedynamic instruction 作为它指定的 target. 每次当这个特别的 instruction 被执行的时候, JVM 就能调用它的 target method handle. 有意思的是, 这个被指定个 invokedynamic instruction 的 target 能够在动态语言发生变化时同时改变.</p>
<p>另一个这个 linkage mechanism 引入的重要组成部分是, bootstrap method。一旦碰到 invokedynamic instruction , 当 instruction 被关联起来的时候, bootstrap method 就会被调用。它会决定哪个 target method 应该被使用。每一个包含invokedynamic 指令的类都必须申明一个 bootstrap method。</p>
<p>总的来说, method handles 提供了一种新的关联机制. 能够让 JVM 在碰到 invokedynamic 的时候, 调用正确的方法.  比较射的方式,  反射需要增加一个模拟层, 这会增加额外的复杂度和过多的操作. 比较起来新机制, 提供了一种忽略方法类型和位置的连接, 支持类型安全并保证了本地执行速度.</p>
<p>&nbsp;</p>
