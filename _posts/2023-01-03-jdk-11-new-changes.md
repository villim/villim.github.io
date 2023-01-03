---
title: JDK 11 New Changes
layout: post
---

After switching projects from JDK 8 to Amazon Corretto 11 (JDK11). It's time to start using new features.

JDK 11 contains quite alot of changes, here just listing some main of coding aspect.


![jdk 8 to 11](http://villim.github.io/img/2023/java-8-11.png)

## 1. Jshell

Java REPL application name is jshell. JShell stands for Java Shell. jshell is an interactive tool to execute and evaluate java simple programs like variable declarations, statements, expressions, simple Programs etc. 

```bash
➜  ~ jshell
|  Welcome to JShell -- Version 11.0.15
|  For an introduction type: /help intro

jshell> int a = 10
a ==> 10

jshell> int b = 20
b ==> 20

jshell> System.out.println("a+b=" + (a+b))
a+b=30
```
  
        
## 2. Improved String

Since Java 9, changed to store with bype[], not char[] anymore.

```java
    @Stable
    private final byte[] value;
```

The purpose is to reduce memory cost, to make sure length calculation correctly, added new field ``coder``. when contains only Lation-1 characters, coder = 0, otherwise coder = 1;

```java
    /**
     * The identifier of the encoding used to encode the bytes in
     * {@code value}. The supported values in this implementation are
     *
     * LATIN1
     * UTF16
     *
     * @implNote This field is trusted by the VM, and is a subject to
     * constant folding if String instance is constant. Overwriting this
     * field after construction will cause problems.
     */
    private final byte coder;
```

## 3. New methods in String

### 3.1 strip(): can remove leading and trailing whitespace characters. The difference with trim() is, it will remove unicode whitespace characters.

```java 
char uwc = '\u2000'; //Unicdoe whitespace character
String str = uwc + "abc" + uwc;
System.out.println(str.strip());
System.out.println(str.trim());

System.out.println(str.stripLeading()); 
System.out.println(str.stripTrailing());
```

### 3.2 isBlank(): Returns true if the string is empty or contains only white space codepoints, otherwise false

```bash
jshell> String str = " ";
jshell> System.out.println(str.isBlank());
true
``````

### 3.3 repeat()

```bash
jshell> String str = "monkey";
jshell> System.out.println(str.repeat(4));
monkeymonkeymonkeymonkey
```


## 4. Collections Factories

We were using java.util.Collections, java.util.ArrayList ... to create a collection of objects quickly.
Now we can use the static method defined in interface.

```java
Set<String> set = Set.of("a","b","c");
var list = List.of("x","y");
Map map1 = Map.of("key1", "value1","key2","value2");
Map map2 = Map.ofEntries(Map.entry("key1","value1"),Map.entry("key2","value2"));
```

one thing need notice is, it generates Immutable Collection in this way:

```bash
jshell> map2.getClass()
$17 ==> class java.util.ImmutableCollections$MapN
```


## 5. var Keyword

Since Java 10, introduced Local Variable Type Inference (LVTI), otherwise known as **var**. It allows the develper to infer they type of variables, instead of the type of values.

```java
var names = new ArrayList<String>();
var newObj = new Object();
var newName = "jack";
var newAge = 10;
var newMoney = 88888888L;
```

* we can still use var as the name of a variable, method, or package.
* Type intention of var is local, and in the case of var, the algorithm examines only the declaration of the local variable. This means it cannot be used for fields, method arguments, or return types.
* var is implemented solely in the source code compiler (javac) and has no runtime or performance effect whatsoever.

    

## 6. Private method in Interface

```java
public interface MyInterface {

    private void privateMethod() {
        System.out.println("123");
    }

    default void defaultMethod() {
        privateMethod(); // invoke private method
    }
}
```

## 7. Improved try-catch

```java
  FileInputStream fis = new FileInputStream("abc.txt");
  FileOutputStream fos = new FileOutputStream("def.txt");
        
  try (fis; fos) { // use ; to split multiple resources
    
  } catch (IOException e) {
    e.printStackTrace();
  }
```    


## 8. Singel-file source-code programs

Before JDK 11, we have to compile before running our program:

```bash
javac HelloWorld.java
java HelloWorld
```

Since JDK 11, we can do:

```bash
java HelloWorld.java
```

* It is limited to code that lives in a single source file
* It cannot compile additional source files in the same run
* It may contain any number of classes in the source file
* It must hae the first class declared in the source file as the entry point
* It must define the main method in the entry point class



   
   
## 9. HTTP/2 Support

* New designed APIs under java.net.http
* New API supports HTTP 1.1 as well as HTTP/2 and can fallback to HTTP 1.1 when a server being called dosn't support HTTP/2
* Most significant benefits of HTTP/2 is its built-in multiplexing

```java
 var client = HttpClient.newBuilder().build();

 var uri = new URI("http://google.com");
 var request = HttpRequest.newBuilder(uri).build();

 var handler = HttpResponse.BodyHandlers.ofString();
 CompletableFuture.allOf(
         client.sendAsync(request, handler).thenAccept((resp) -> System.out.println(resp.body())),
         client.sendAsync(request, handler).thenAccept((resp) -> System.out.println(resp.body())),
         client.sendAsync(request, handler).thenAccept((resp) -> System.out.println(resp.body()))
 ).join();
```



## 10. Java Modules

A **module** is a fundamentally new concept in the Java language since JDK 9. It is a unit of application deployment and dependency that has semantic meaning to the runtime. It is different from previous existing concepts for following reasons:

* JAR files are invisible to the runtime
* Packages just namespaces to group classes togehter for access control
* Dependencies are defined at the class level only
* Access control and reflection combine in a way that produces a fundamentally open system without clear deployment unit boundaries and with minimal enforcement.

Modules, on the other hand:

* Define dependency information between modules, so all sorts of resolution and linkage problems can be detected at compile or application start time
* Provide proper encapsulation, so internal packages and classes can be make safe from pesky users who might want to fiddle with them
* Are a proper unit of deployment with metadata that can be understood and consumed by a  modern Java runtime and are represented in the Java type system.

... ...

Should we start using Modules? 

[Answer by Mark Reinhold](https://stackoverflow.com/questions/62950667/is-there-any-need-to-switch-to-modules-when-migrating-to-java-9-or-later/62959016#62959016) (Chief architect for java at Oracle):

> Java 9 and later releases support traditional JAR files on the traditional class path, via the concept of the unnamed module, and will likely do so until the heat death of the universe.

> Whether to start using modules is entirely up to you.

> If you maintain a large legacy project that isn’t changing very much, then it’s probably not worth the effort.

> If you work on a large project that’s grown difficult to maintain over the years then the clarity and discipline that modularization brings could be beneficial, but it could also be a lot of work, so think carefully before you begin.

> If you’re starting a new project then I highly recommend starting with modules if you can. Many popular libraries have, by now, been upgraded to be modules, so there’s a good chance that all of the dependencies that you need are already available in modular form.

> If you maintain a library then I strongly recommend that you upgrade it to be a module if you haven’t done so already, and if all of your library’s dependencies have been converted.


## Read more: 

* [Book: The Java Module System](https://www.manning.com/books/the-java-module-system)
* [Migrating from Java 8 to Java 11 – A Guide Note](https://inapp.com/blog/migrating-from-java-8-to-java-11-a-guide-note/)