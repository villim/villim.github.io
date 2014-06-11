---
layout: post
title: A Interesting Problem About Overriding Variables
categories:
- JAVA
tags:
- Java

---

#Variables can also be overridden
It’s known as shadowing or hiding. But when variables are overridden what will happen? 

Look at the codes below, S1 and S2 are parent and child relationship:

{% highlight Java %}

class S1 {
	public String s = "S1";
	public String getS() {
		return s;
	}
}

class S2 extends S1{
	public String s = "S2";
	public String getS() {
		return s;
	}
}
{% endhighlight %}

And let's initialize them in following way:

{% highlight Java %}
S1 s1 = new S1();
S2 s2 = new S2();
System.out.println(s1.s); //print 1
System.out.println(s1.getS()); //print 2
System.out.println(s2.s); //print 3
System.out.println(s2.getS()); //print 4

s1 = s2;
System.out.println(s1.s);//print 5
System.out.println(s1.getS()); //print 6
{% endhighlight %}


# What is 5 and 6 print out?


"S1" or "S2" ? 
You can think a while first ~ ~

the resulet is:

** //print 5 -------  'S1' **

** //print 6 -------  'S2' **



Is that your answer? 
Do you know why? At first glance, we may think,after s1= s2, s1 have point to  the instance of  S2, and s2.s = "S2",so the result is "S2". Then  how can it  be "S1" ?

As we know " ** variable is resolved at compile time ** and ** method is resolved at run time ** .  

When we upcast S2 to S1 in the line "S1=S2", To S1.s , S2.s is a shadow  field. when S1 initialised, it don't  know the existance of S2.s. cuz S2.s is resolved at compile time. So //print 5 will return "S1".

but at  // print 6. It's quite different when we call method s1.getS(). Cuz S2 orverriding getS()  method, and ** method is resolved at run time **, so we can get "S2".

if we define S2 like this :

{% highlight Java %}

class S2 extends S1{
	public String s = "S2";
	public String getS() {
	return super.getS();
}


{% endhighlight %}

will print "S1" at // print 6, cuz to the parent method getS(), it  doesn't know S2.s exist.</span></span></span>
