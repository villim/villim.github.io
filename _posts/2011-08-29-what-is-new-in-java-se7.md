---
layout: post
title: What's new in Java SE7
categories:
- JAVA
tags:
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
<p>SUN这个悲剧破产过程，让一切都变得拖拖拉拉，混乱不堪，从2010年说到2011年，终于 Java7 来了。好死不死的 JAVA 也该加把火了。Oracle 是不是个好 “东家”，不是一朝一夕能够看清楚的。刚发布就出了HotSpot Loop optimizations的BUG，把JVM搞崩溃。不过还算发现即时，当然现在的 7  可能还不是开发的最佳选择，但是 Java7 到底有什么新鲜的玩意儿呢？</p>
<h3><span style="color: #008000;"><strong>Switch 增加了对字符串的支持</strong></span></h3>
<pre class="brush:java">	String str = "abc";
	switch (str) {
	case "abc":
		System.out.println("yes");
		break;
	case "efg":
		System.out.println("no");
		break;
	default:
		break;
	}</pre>
<p>这个对代码的影响还是很大的。有很多 ELSE IF 都能得到简化。</p>
<h3><span style="color: #008000;"><strong>Try-with-Resources</strong></span></h3>
<p>先看一段1.6 版本里的写法：</p>
<pre class="brush:java">	File file = new File("test.xml");
	InputStream is = null;

	try{
		is = new FileInputStream(file);
	}catch(FileNotFoundException e){
		System.err.println("Missing file " + file.getAbsolutePath());
	}catch(IOException e){
	        System.err.println("Missing file " + file.getAbsolutePath());
        }finally{
		if(is != null){
			is.close();
		}
	}</pre>
<p>Java7 里我们怎么做呢？</p>
<pre class="brush:java">	File file = new File("D://test.txt");
	try(FileInputStream is = new FileInputStream(file)){
		//do something
	}catch(IOException | NullPointerException e){
		System.err.println("Missing file " + file.getAbsolutePath());
	}</pre>
<p><strong>Try-with-resources</strong> 里的资源能够自动释放了，不用繁琐的写 finally 了。另外 <span style="color: #ff0000;"><strong>“|”</strong></span> 能够简化无聊的一大段拷贝代码。Sonar Check 应该很乐于看到这样的代码简化吧。</p>
<h3><span style="color: #008000;"><strong>Rethrowing Exceptions with More Inclusive Type Checking</strong></span></h3>
<p>在1.6 版本里，我们在方法的 throws 里面无法丢出 FirstException 和 SecondException , 如果你尝试这么做，会得到这样的错误信息 "unreported exception Exception; must be caught or declared to be thrown"。 因为catch块里捕获了 Exception。</p>
<pre class="brush:java">	static class FirstException extends Exception {}
	static class SecondException extends Exception {}

	public void rethrowException(String exceptionName) throws Exception {
		try {
			if (exceptionName.equals("First")) {
				throw new FirstException();
			} else {
				throw new SecondException();
			}
		} catch (Exception e) {
			throw e;
		}
	}</pre>
<p>Java 7 里面，你可以无视 catch 块直接抛出 FirstException 和 SecondException：</p>
<pre class="brush:java">	public void rethrowException(String exceptionName) throws FirstException,
			SecondException {
		try {
			// ...
		} catch (Exception e) {
			throw e;
		}
	}</pre>
<p>Java7 的编译器，可以辨别出 “e” 是<code>FirstException</code> 或者 <code>SecondException</code>的实例。在7和以后的版本中，当你再catch块中捕获一个或者多个异常类型，并重新抛出时，编译器会检查这些异常的类型是否满足下面的要求：</p>
<ul>
<li>Try 块能够抛出这些异常</li>
<li>没有其他更优先的catch块已经能捕获它</li>
<li>它是某一个catch块参数的 subtype 或者 supertype</li>
</ul>
<p>拿这里来说，能够抛出 FirstException 和 SecondException 的原因是他们是 Exception 的 subtype.</p>
<p>&nbsp;</p>
<h3><span style="color: #008000;"><strong>改善了针对泛型实例创建</strong></span></h3>
<p>可以将：</p>
<pre class="brush:java">Map&lt;String, List&lt;String&gt;&gt; anagrams = new HashMap&lt;String, List&lt;String&gt;&gt;();</pre>
<p>简化成：</p>
<pre class="brush:java">Map&lt;String, List&lt;String&gt;&gt; anagrams = new HashMap&lt;&gt;();</pre>
<p>&nbsp;</p>
<h3><span style="color: #008000;"><strong>数字增加了二进制表示和下划线分隔符</strong></span></h3>
<p>先来看看二进制表示：</p>
<pre class="brush:java">byte b = 0b001_00001;
short s = 0b001001001001;
int i = 0b001001001001001;</pre>
<p>再来看看下划线：</p>
<pre class="brush:java">int i = 123_3457;
long l = 123_2983L;
long maxLong = 0x7fff_ffff_ffff_ffffL; // 二进制表示</pre>
<p>毫无疑问，下划线能够增强可读性，但是有几个不适用的地方：</p>
<ul>
<li>不能用在数字的开头</li>
<li>不能用在小数点的左边或者右边</li>
<li>不能用在Long或者Float型的后缀符F或者L的左边或者右边</li>
<li>不能拆散二进制八进制十六进制数字 比如原本的0X被拆成0_X</li>
</ul>
<p>&nbsp;</p>
<h3><span style="color: #008000;"><strong>两个主要的新API</strong></span></h3>
<p><span style="color: #993300;"><strong>第一个</strong> 是JSR 203</span>，针对文件系统访问、可扩展异步I/O操作、多播数据包、Socket通道绑定和配置添加了新的API。企业开发者特别感兴趣的是增加了真正的异步I/O API，这对需要跨多连接的低延时、高吞吐的高端服务器应用程序来说尤为重要。JSR 203还为Java添加了一个真的文件系统API，提供了对某些OS特定功能的支持。例如，你可以在支持符号链接的系统中创建符号链接。但这一特性也备受争议，虽然JSR 203提供了可运行于所有平台、支持平台特定特性的通用API，但它并非严格意义上的“一次编写到处运行”。</p>
<p><span style="color: #993300;"><strong>第二个</strong> 新API是Fork/Join框架（JSR 166的一部分）</span>，起初是计划放在Java 5里的。它为开发者提供了一种机制，可以将问题拆解为多个任务，在任意数量的处理器核心上并行执行。</p>
<p>&nbsp;</p>
<h3><span style="color: #008000;"><strong>新的字节码指令 ： InvokeDynamic</strong></span></h3>
<p>为了支持越来越多在 JVM 上跑的动态语言。Java SE 7使用了InvokeDynamic关键字来标记Java诞生后的首个新字节码指令。InvokeDynamic添加了一种新的调用模式和链接模式，可以通过编程支持用户定制的规范。特别是在缺乏静态类型信息的方法调用中，它能支持高效、灵活的方法执行，这大幅改善了动态语言的性能，例如运行于JVM之上的JRuby和Jython。</p>
<p>新的 <span style="color: #666699;"><strong>invokedynamic</strong></span> 字节码指令的语法与 <strong>invokeinterface</strong> 指令类似：</p>
<pre class="brush:java">invokedynamic &lt; method-specification&gt; &lt; n&gt;</pre>
<p><strong>invokeinterface</strong> 字节码指令差不多是这样：</p>
<pre class="brush:java">invokedynamic #10;
//DynamicMethod java/lang/Object.lessThan：(Ljava/lang/Object;)</pre>
<p><em><span style="color: #666699;">invokedynamic</span> 的区别就在于它的 &lt; method-specification&gt; 只需指定方法名称，对描述符的唯一要求是它应引用非空对象。</em>invokedynamic 字节码指令运行动态语言的实现器(implementer)将方法调用编译为字节码，而不必指定目标的类型，该目标包含了方法、调用的返回类型或方法参数类型。这些类型对于执行指令的 JVM 不必是已知的。</p>
<p>问题来了，如果未提供接收器的类型，JVM 该如何找到该方法? 答案在于，JSR 292 还包含了一个新的动态类型语言的连接机制。JVM 使用新的连接机制获取所需的方法。</p>
<p><span style="color: #993300;"><strong>新的动态连接机制：方法句柄(method handle)</strong></span></p>
<p>JDK 7 包含了新包，java.dyn，其中包含了与在 Java 平台中动态语言支持相关的类。其中一个类为 MethodHandle.方法句柄是类型 java.dyn.MethodHandle 的一个简单对象，该对象包含一个 JVM 方法的匿名引用。</p>
<p>新连接机制还包含一个<strong>bootstrap 方法</strong>，它是一个方法句柄，决定了call site 调用的目标方法。Call site 是调用指令的实例，这里它就是 invokedynamic 字节码指令的实例。包含 invokedynamic 指令的每个类都必须指定 bootstrap 方法。</p>
<p>JVM 第一次遇到具有接收器和参数的 invokedynamic 字节码时，它调用 bootstrap方法。（调用语言支持的方法，可以使用术语 up-call 来描述。）</p>
<p>bootstrap方法反过来选择相应的目标方法句柄。然后 JVM 将该方法句柄引用的方法与 invokedynamic 字节码关联起来。JVM 下次遇到具有相同接收器和参数的 invokedynamic 字节码时，它将立即调用之前所选的方法。</p>
<p><span style="color: #993300;"><strong>方法句柄</strong></span>相当简单，仅包含一个描述特定类型的 type toke。此外，方法句柄隐式地包含一个与其关联的 invoke 方法。要调用方法句柄，你需要调用它的 invoke 方法，与调用对象方法类似，即 MethodHandle.invoke(……)。由于每个方法句柄都具有其自身的类型，因此，它只接受那个类型的 invoke 调用。如果调用的类型与方法句柄的类型不匹配，方法句柄将返回异常。 <em></em></p>
<p><strong><em>总之，方法句柄提供了一种连接机制，它能够让 JVM 根据 invokedynamic 字节码指令调用正确的方法。但 JVM 遇到 invokedynamic 字节码时，它将使用方法句柄获得所需的方法。</em></strong></p>
<p><em></em>请注意，相对于映射调用，方法句柄提供了一种更好的方式，来满足方法调用的字节码要求。相较而言，方法句柄提供了一种命名和连接方法的方式，而无需考虑方法类型或位置，而且这种方式具有完善的类型安全和本地的执行速度。</p>
<h3><span style="color: #008000;"><strong>其他</strong></span></h3>
<p>新的网络和安全特性，对国际化的扩展支持中还包括了Unicode 6.0支持，等</p>
