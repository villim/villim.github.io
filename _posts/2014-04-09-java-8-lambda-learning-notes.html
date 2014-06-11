---
layout: post
title: Java 8 Lambda Learning Notes
categories:
- JAVA
tags:
- Java8
- Lambda
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
<p>Java8 could be the most interesting  release during these years,  it will definitely change the way people writing code, and it also need some effort for the older Java developers to familiar the new style.</p>
<p>After this Lambda is introduced to Java, it really have hug impact on previous Java Philosophy. Not only the FUNCTIONAL PROGRAMMING style, in order to accomplish this also making Java able to do Multiple Inheritance! That's something! But in this page, let's look at Lambda itself first.</p>
<p>Read a lot of documents, I found <a title="Java 8 Lambdas" href="http://www.amazon.cn/Java-8-Lambdas-Pragmatic-Functional-Programming-Warburton-Richard/dp/1449370772/" target="_blank"><em><strong>Java 8 Lambdas: Pragmatic Functional Programming</strong></em> </a>is a very good start to know what is Java 8 Lambda. Here's just the notes for what I learned.</p>
<h3><span style="color: #993300;"><strong>What is Lambda</strong></span></h3>
<p>--------------------------------------------------------------</p>
<p><b>Argument List      <b>Arrow Token        <b>Body</b></b></b></p>
<p><span style="color: #339966;"><strong>(int x, int y)                -&gt;                  x + y</strong></span></p>
<p>--------------------------------------------------------------</p>
<p>it composed with 3 parts. Let's see more examples:</p>
<ul>
<li><span style="color: #339966;"><strong>() -&gt; 42</strong></span></li>
<li><span style="color: #339966;"><strong>(String s) -&gt; { System.out.println(s); }</strong></span></li>
<li><span style="color: #339966;"><strong>() -&gt; { return 3.1415 };</strong></span></li>
</ul>
<p>what we can see is:</p>
<ol>
<li>The body can be either a single expression or a statement block.</li>
<li>can specify Type for parameter in Argument List</li>
<li>In the expression form, the body is simply evaluated and returned. In the block form, the body is evaluated like a method body and a return statement returns control to the caller of the anonymous method.</li>
<li>The break and continue keywords are illegal at the top level, but are permitted within loops. If the body produces a result, every control path must return something or throw an exception.</li>
</ol>
<p>&nbsp;</p>
<h3><span style="color: #993300;"><strong>Functional Interface</strong></span></h3>
<p>Let's look at  how we usually using Runnalbe Interface at first,</p>
<pre class="brush:java">		
// AnonymousRunnable
Runnable r1 = new Runnable() {
    @Override
    public void run() {			
        System.out.println("Helloworldone!"); 
    }
};</pre>
<p>Runnable interface has only one abstract method which is run(), in Java8 it is defined as following</p>
<pre class="brush:java">@FunctionalInterface
public interface Runnable {
    public abstract void run();
}</pre>
<p>And this kind of interface is called <span style="color: #339966;"><strong>Functional Interface : </strong><em>A functional interface is an interface with a single abstract method that is used as the type of a lambda expression.  </em></span>After using <strong>@FunctionalInterface </strong>to indicate,<strong> </strong>Java will do compile check for it. So if it's a Functional Interface, we can write the code in this way in Java8.</p>
<pre class="lang:java decode:true">//LambdaRunnable21     
Runnable r2 =()-&gt; System.out.println("Helloworldtwo!");</pre>
<p><span style="line-height: 1.6em;">In the same way, the listener in  GWT will be greatly simplified like following</span></p>
<pre class="lang:java decode:true">JButton testButton = new JButton("Test Button");
testButton.addActionListener(
    new ActionListener() {
	@Override
	public void actionPerformed(ActionEvent ae) {
		System.out.println("Click Detected by Anon Class");
     }
});

//Lambda Express
testButton.addActionListener(e -&gt; System.out.println("Click Detected by Lambda Listner"));</pre>
<p><span style="line-height: 1.6em;">We already see that we can pass a lambda express as parameter to a Method, every Java parameter has a type, but what is the Type of a Lambda?</span></p>
<h3><strong><span style="color: #993300;">What is the type of Lambda</span></strong></h3>
<p>In java.util.function package, Java8 bring some new stuff, you should read the Javadoc carefully to see how they works.</p>
<ul>
<li>Predicate: A property of the object passed as argument</li>
<li>Consumer: An action to be performed with the object passed as argument</li>
<li>Function: Transform a T to a U</li>
<li>Supplier: Provide an instance of a T (such as a factory)</li>
<li>UnaryOperator: A unary operator from T -&gt; T</li>
<li>BinaryOperator: A binary operator from (T, T) -&gt; T</li>
</ul>
<p>Let's Just use a simple example to illustrate how predicate and Consumer works</p>
<pre class="lang:java decode:true">public static Student updateStudentFee(Student student,
      Predicate&lt;Student&gt; predicate,
      Consumer&lt;Student&gt; consumer){

    //Use the predicate to decide when to update the discount.
    if ( predicate.test(student)){
      //Use the consumer to update the discount value.
      consumer.accept(student);
    }
    return student;
}

Student student1 = new Student("Villim","Wong", 9.5);
student1 = updateStudentFee(student1,
       //Lambda expression for Predicate interface
       student -&gt; student.grade &gt; 8.5,
       //Lambda expression for Consumer inerface
       student -&gt; student.feeDiscount = 30.0);</pre>
<p>&nbsp;</p>
<p>When you checking the source code of Function you will find it like this</p>
<pre class="lang:java decode:true">@FunctionalInterface
public interface Function&lt;T, R&gt; {

    R apply(T t);

    default &lt;V&gt; Function&lt;T, V&gt; andThen(Function&lt;? super R, ? extends V&gt; after) {
        Objects.requireNonNull(after);
        return (T t) -&gt; after.apply(apply(t));
    }

    static &lt;T&gt; Function&lt;T, T&gt; identity() {
        return t -&gt; t;
    }
}</pre>
<p><span style="line-height: 1.6em;">we can learn several things here</span></p>
<ul>
<li>Function has 3 methods, because the definition says ONLY ONE SINGLE ABSTRACT METHOD, and you don't need explicit specify abstract to it.</li>
<li><span style="color: #008000;">Methods can be static</span> now ! A common scenario in Java libraries is, for some interface <code>Foo</code>, there would be a companion utility class <code>Foos</code> with static methods for generating or working with Foo instances. Now that static methods can exist on interfaces, in many cases the <code>Foos</code> utility class can go away (or be made package-private), with its public methods going on the interface instead.</li>
<li>And the last but more important is , <span style="color: #008000;">methods can have <strong>default</strong> implementation</span> now ! This the the way, Java8 is able to compatible to previous 1-7 versions. And it also bring a new thing that break  Java principle which was advertised as a advantage concept to C++, Multiple Inheritance. And we wanna ask another question too, what's the difference with Abstract Class ?</li>
</ul>
<h3><span style="color: #993300;"><strong>Java8 Interfaces And Abstract Classes</strong></span></h3>
<p>Both of them can have method implementation now, but It’s also pretty clear that there’s still a distinction . Interfaces give you multiple inheritance but no fields, while abstract classes let you inherit fields but you don’t get multiple inheritance.</p>
<p>Of course, when modelling your problem domain, you need to think about this tradeoff, which wasn’t necessary in previous ver‐ sions of Java.</p>
<h3><span style="color: #993300;"><strong>Multiple Inheritance</strong></span></h3>
<p>Basically, Java become DANGEROUS too now, if you can't understand the language well. But you can't have your cake and eat it too. Programming is never a easy work that everybody can do. The other hand, the benefit is more valuable.</p>
<p>When these interfaces have a same method signature method, it will becoming tricky, like this</p>
<pre class="brush:java">public interface Jukebox {
    public default String rock() {
        return "... all over the world!"; 
     }
}

public interface Carriage {
    public default String rock() { 
        return "... from side to side";
    }
}

public class MusicalCarriage implements Carriage, Jukebox { }</pre>
<p>Java compiler won't know which one should be invoked, and will give Error. You can solve it in this way</p>
<pre class="brush:java">public class MusicalCarriage implements Carriage, Jukebox {
   @Override
   public String rock() {
       return Carriage.super.rock();
   } 
}</pre>
<p>There're <span style="color: #339966;"><strong>Three Rules  to Remember</strong></span></p>
<div title="Page 67">
<p>If you’re ever unsure of what will happen with default methods or with multiple in‐ heritance of behavior, there are three simple rules for handling conflicts:</p>
</div>
<div title="Page 68">
<ol>
<li>Any class wins over any interface. So if there’s a method with a body, or an abstract declaration, in the superclass chain, we can ignore the interfaces completely.</li>
<li>Subtype wins over supertype. If we have a situation in which two interfaces are competing to provide a default method and one interface extends the other, the subclass wins.</li>
<li>No rule 3. If the previous two rules don’t give us the answer, the subclass must either implement the method or declare it abstract.</li>
</ol>
<p>Rule 1 is what brings us compatibility with old code.</p>
<p>&nbsp;</p>
<h3><span style="color: #993300;"><strong>Lambda use Value</strong></span></h3>
<p>one last thing is when Lambda manipulate value, we need be careful,</p>
<pre class="lang:java decode:true ">String name = getUserName();
button.addActionListener(event -&gt; System.out.println("hi " + name));

String name = getUserName();
name = formatUserName(name);
// will throw Exception
button.addActionListener(event -&gt; System.out.println("hi " + name));</pre>
<p><span style="line-height: 1.6em;">local variables referenced from a lambda expression must be final or effectively final.  Java didn't force use to announce it final just for friendly.</span></p>
</div>
<h3><span style="color: #993300;"><strong>Method Reference</strong></span></h3>
<div title="Page 73">
<p>A common idiom you may have noticed is the creation of a lambda expression that calls a method on its parameter. If we want a lambda expression that gets the name of an artist, we would write the following:</p>
<pre class="lang:java decode:true ">    artist -&gt; artist.getName()</pre>
<p><span style="line-height: 1.6em;">This is such a common idiom that there’s actually an abbreviated syntax for this that lets you reuse an existing method, called a method reference. If we were to write the previous lambda expression using a method reference, it would look like this:</span></p>
<pre class="brush:java">    Artist::getName</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>As Lambda coming, it greatly changed how we use Collection. And Collection is another big part of Java8. It's such a monster, let's make another note later.</p>
<p>------------------------------------------------------------------------</p>
<p>P.S.</p>
<p>In order to practise Java8 you need prepare following stuff:</p>
<p><strong>Java Development Kit (JDK 8) early access</strong><br />
<strong> NetBeans 7.4 | Elcipse 4.3.2 | STS 3.5.0</strong></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
