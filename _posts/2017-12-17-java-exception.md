---
title: Java Exception
layout: post
---

Whether we should extends our customized exception from **Exception** or **RuntimeException** is always a intreseting question for Java programmers.

## Exception & RuntimeException

First we should know the very basic knowledge of Java Excpeiton.

**Excpetion** is the root of all the excpetions, it indicates conditions that a reasonable application might want to catch. The Excpetion and it's subclasses have to decaled in method **throws** clause, otherwise we have to handle it in **TRY-CATCH** clause. Sometime, we also call it **Checked Exception**.

**RuntimeException** extends from Exception, but it's quite different, it'ssuperclasses can be thrown during the normal operation of the Java Virtual Machine. That means we don't need to **throws** in method definition or **TRY-CATCH** it. The most usually encountered RuntimeException is NullPointerException, it can be thrown out anywhere when JVM find a method invoked on a Null Object. We call this kind of exception also **Unchecked Exception**.

## How to define our Excpeiton?

The most intuitive thinking is, Checked Exception require be throws at method signature, and invoked methods have to handle these excpeitons. When there are quite many Checked Exception, it's really making it less readable and hard to use.

While Unchecked Exception from From the perspective of code, it's very very clean, no need to **throws**, no need to handle. It will automatically be thrown out by JVM. However, you won't know where may cause problems, thus you won't be able to prevent error from happening.


## Programming Error & Logic Error

To think this problem in semantic way, we may get a better understanding.

Our code have two kinds of Errors, **Programming Error** and **Logic Error**. NullPointerException is the most typical Programming Error, it should happened at all if we are careful enough.  While Logic Error is the errors that constrainted with our business logic rules. ***Hardcore Java*** suggested:

* If an exception is always the result of a programming error, make it a direct descendant of RuntimeException.
* If an exception represents a user's failure to enter data properly, you may be able to get away with using RuntimeException. This will allow you to propagate the RuntimeException in business logic classes without having to declare it. However, the GUI or other interface to the program should always watch for these kinds of errors. 
* If the exception is always the result of a business logic error, make it a direct descendant of Exception and use exception filtering when appropriate.





