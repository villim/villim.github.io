---
layout: post
title: Java 8 Lambda Learning Notes
categories:
- JAVA
tags:
- Java8
- Lambda

---
Java8 could be the most interesting  release during these years,  it will definitely change the way people writing code, and it also need some effort for the older Java developers to familiar the new style.

After this Lambda is introduced to Java, it really have hug impact on previous Java Philosophy. Not only the FUNCTIONAL PROGRAMMING style, in order to accomplish this also making Java able to do Multiple Inheritance! That's something! But in this page, let's look at Lambda itself first.

Read a lot of documents, I found <a title="Java 8 Lambdas" href="http://www.amazon.cn/Java-8-Lambdas-Pragmatic-Functional-Programming-Warburton-Richard/dp/1449370772/" target="_blank">**Java 8 Lambdas: Pragmatic Functional Programming** </a>is a very good start to know what is Java 8 Lambda. Here's just the notes for what I learned.

###What is Lambda

> (int x, int y) ->  x + y 

it composed with 3 parts: **Argument List, Arrow Token and Body**. Let's see more examples:

*  **() -> 42**
*  **(String s) -> { System.out.println(s); }**
*  **() -> { return 3.1415 };**

what we can see is:

1. *The body can be either a single expression or a statement block.*
2. *can specify Type for parameter in Argument List*
3. *In the expression form, the body is simply evaluated and returned. In the block form, the body is evaluated like a method body and a return statement returns control to the caller of the anonymous method.*
4. *The break and continue keywords are illegal at the top level, but are permitted within loops. If the body produces a result, every control path must return something or throw an exception.*

###Functional Interface
Let's look at  how we usually using Runnalbe Interface at first,
{% highlight Java %}

	// AnonymousRunnable
	Runnable r1 = new Runnable() {
    	@Override
    	public void run() {			
        	System.out.println("Helloworldone!"); 
	    }
	};
{% endhighlight %}

Runnable interface has only one abstract method which is run(), in Java8 it is defined as following
{% highlight Java %}

	@FunctionalInterface
		public interface Runnable {
    	public abstract void run();
	}
{% endhighlight %}

And this kind of interface is called <span style="color: #339966;">**Functional Interface** : *A functional interface is an interface with a single abstract method that is used as the type of a lambda expression.*  </span> 


After using **@FunctionalInterface** to indicate, Java will do compile check for it. So if it's a Functional Interface, we can write the code in this way in Java8.
{% highlight Java %}

	//LambdaRunnable21     
	Runnable r2 =() -> System.out.println("Helloworldtwo!");
{% endhighlight %}

In the same way, the listener in  GWT will be greatly simplified like following
{% highlight Java %}

	JButton testButton = new JButton("Test Button");
	testButton.addActionListener(
    	new ActionListener() {
		@Override
		public void actionPerformed(ActionEvent ae) {
			System.out.println("Click Detected by Anon Class");
	     }
	});
{% endhighlight %}

By using Lambda Express, it can be simplify as:
{% highlight Java %}

	testButton.addActionListener(e -> System.out.println("Click Detected by Lambda Listner"));
{% endhighlight %}	

We already see that we can pass a lambda express as parameter to a Method, every Java parameter has a type, but what is the Type of a Lambda?

###What is the type of Lambda
In java.util.function package, Java8 bring some new stuff, you should read the Javadoc carefully to see how they works.

* Predicate: A property of the object passed as argument</li>
* Consumer: An action to be performed with the object passed as argument</li>
* Function: Transform a T to a U</li>
* Supplier: Provide an instance of a T (such as a factory)</li>
* UnaryOperator: A unary operator from T -> T</li>
* BinaryOperator: A binary operator from (T, T) -> T</li>


Let's Just use a simple example to illustrate how predicate and Consumer works.
{% highlight Java %}

	public static Student updateStudentFee(Student student,
      Predicate<Student> predicate,
      Consumer<Student> consumer){

    	//Use the predicate to decide when to update the discount.
    	if ( predicate.test(student)){
      	  //Use the consumer to update the discount value.
      	  consumer.accept(student);
    	}
    	return student;
	}
	
	Student student1 = new Student("Villim","Wong", 9.5);
	student1 = updateStudentFee(student1,
      student -> student.grade > 8.5,//Lambda expression for Predicate interface
      student -> student.feeDiscount = 30.0);//Lambda expression for Consumer inerface
{% endhighlight %}	

When you checking the source code of Function you will find it like this
{% highlight Java %}

	@FunctionalInterface
	public interface Function<T, R> {
    	R apply(T t);
	    default <V> Function<T, V> andThen(Function<? super R, ? extends V> after) 		{
        	Objects.requireNonNull(after);
	        return (T t) -> after.apply(apply(t));
    	}

    	static <T> Function<T, T> identity() {
    	    return t -> t;
    	}
	}
{% endhighlight %}

we can learn several things here:

* Function has 3 methods, because the definition says ONLY ONE SINGLE ABSTRACT METHOD, and you don't need explicit specify abstract to it.

* <span style="color: #008000;">**Methods can be static**</span> now ! A common scenario in Java libraries is, for some interface `Foo`, there would be a companion utility class `Foos` with static methods for generating or working with Foo instances. Now that static methods can exist on interfaces, in many cases the `Foos` utility class can go away (or be made package-private), with its public methods going on the interface instead.

* And the last but more important is , <span style="color: #008000;">methods can have **default** implementation</span> now ! This the the way, Java8 is able to compatible to previous 1-7 versions. And it also bring a new thing that break  Java principle which was advertised as a advantage concept to C++, Multiple Inheritance. And we wanna ask another question too, what's the difference with Abstract Class ?

###Java8 Interfaces And Abstract Classes

Both of them can have method implementation now, but It’s also pretty clear that there’s still a distinction . Interfaces give you multiple inheritance but no fields, while abstract classes let you inherit fields but you don’t get multiple inheritance.

Of course, when modelling your problem domain, you need to think about this tradeoff, which wasn’t necessary in previous ver‐ sions of Java.

###Multiple Inheritance

Basically, Java become DANGEROUS too now, if you can't understand the language well. But you can't have your cake and eat it too. Programming is never a easy work that everybody can do. The other hand, the benefit is more valuable.

When these interfaces have a same method signature method, it will becoming tricky, like this
{% highlight Java %}

	public interface Jukebox {
    	public default String rock() {
        	return "... all over the world!"; 
     	}
	}

	public interface Carriage {
    	public default String rock() { 
        	return "... from side to side";
    	}
	}
	
	public class MusicalCarriage implements Carriage, Jukebox { }
{% endhighlight %}


Java compiler won't know which one should be invoked, and will give Error. You can solve it in this way:
{% highlight Java %}

	public class MusicalCarriage implements Carriage, Jukebox {
		@Override
		public String rock() {
    	   	return Carriage.super.rock();
		} 
	}
{% endhighlight %}

####Three Rules  to Remember

If you’re ever unsure of what will happen with default methods or with multiple in‐ heritance of behavior, there are three simple rules for handling conflicts:


1. Any class wins over any interface. So if there’s a method with a body, or an abstract declaration, in the superclass chain, we can ignore the interfaces completely.

2. Subtype wins over supertype. If we have a situation in which two interfaces are competing to provide a default method and one interface extends the other, the subclass wins.

3. If the previous two rules don’t give us the answer, the subclass must either implement the method or declare it abstract.

**Rule 1 is what brings us compatibility with old code.**


###Lambda use Value

one last thing is when Lambda manipulate value, we need be careful
{% highlight Java %}

	String name = getUserName();
	button.addActionListener(event -> System.out.println("hi " + name));

	String name = getUserName();
	name = formatUserName(name);
	// will throw Exception
	button.addActionListener(event -> System.out.println("hi " + name));
{% endhighlight %}	

local variables referenced from a lambda expression must be final or effectively final. Java didn't force use to announce it final just for friendly.

###Method Reference

A common idiom you may have noticed is the creation of a lambda expression that calls a method on its parameter. If we want a lambda expression that gets the name of an artist, we would write the following:
{% highlight Java %}

	artist -> artist.getName()
{% endhighlight %}

This is such a common idiom that there’s actually an abbreviated syntax for this that lets you reuse an existing method, called a method reference. If we were to write the previous lambda expression using a method reference, it would look like this:
{% highlight Java %}

	Artist::getName
{% endhighlight %}

As Lambda coming, it greatly changed how we use Collection. And Collection is another big part of Java8. It's such a monster, let's make another note later.

---

**P.S.**

In order to practise Java8 you need prepare following stuff:

* Java Development Kit (JDK 8) early access
* NetBeans 7.4 | Elcipse 4.3.2 | STS 3.5.0