---
title: ThreadPool
layout: post
---

## What is ThreadLocal

ThreadLocal 从JDK1.2开始就有了，虽然不是什么很新奇的东西，用起来也简单，可却算得上Java的“高级”技巧，它的使用场景是多线程环境。假如不能很好的理解，当然使用的场景，不能很好的理解Java的线程机制，很容易造成奇怪的BUG。

从名字来理解它的含义，并不是Local Thread，而是Thread Local Variable，就是线程的局部变量。我们可以存放和线程相关的东西，在多线程的环境里，共享数据并保持线程的安全。

## How ThreadLocal Works

每个Thread都有一个ThreadLocalMap的变量, 但是Thread本身并不能操作它，而是交给ThreadLocal管理：

```java
#java.lang.Thread.java

    /* ThreadLocal values pertaining to this thread. This map is maintained
     * by the ThreadLocal class. */
    ThreadLocal.ThreadLocalMap threadLocals = null
```

ThreadLocal 最要的方法就是 set(T) 和 get()，它们做的其实很简单，就是找到对应的线程T，拿出ThreadLocalMap并填值即可。

```java

#java.lang.ThreadLocal.java

    public void set(T value) {
        Thread t = Thread.currentThread();
        ThreadLocalMap map = getMap(t);
        if (map != null)
            map.set(this, value);
        else
            createMap(t, value);
    }

    public T get() {
        Thread t = Thread.currentThread();
        ThreadLocalMap map = getMap(t);
        if (map != null) {
            ThreadLocalMap.Entry e = map.getEntry(this);
            if (e != null) {
                @SuppressWarnings("unchecked")
                T result = (T)e.value;
                return result;
            }
        }
        return setInitialValue();
    }
    
    public void remove() {
         ThreadLocalMap m = getMap(Thread.currentThread());
         if (m != null)
             m.remove(this);
     }
    
```
这里有一点要注意的就是，ThreadLocalMap的Key，并不是Thread本身，而是ThreadLocal.threadLocalHashCode,就是说key和ThreadLocal的instance相关。

```java
#java.lang.ThreadLocal.java

private final int threadLocalHashCode = nextHashCode();
private static AtomicInteger nextHashCode = new AtomicInteger();
private static int nextHashCode() {
	return nextHashCode.getAndAdd(HASH_INCREMENT);
}

```

## What's the Problem ?

### Problem 1: 数据丢失

最常碰到的问题，就是放到ThreadLocal里面的东西找不到了...比如以前把用户登陆信息session，放到ThreadLocal里面，用来判断用户是否登陆。可用户在使用过程中，突然提示未登录。

这里是在配合ThreadPool的使用的时候，出现了问题。现在的Application Sever，比如Jetty、Tomcat，都是使用ThreadPool的。它们不能保证，永远都使用同一个线程服务。于是这里要解决的问题，发生了变化，变成了一个用户，多个线程的问题，可以考虑使用外部存储，在多个线程之间来获得一致的数据。

### Problem 2: 内存溢出

还有一个尝尝被忽略的问题，我们不断地往ThreadLocalMap里面塞东西，塞进去的又都是强引用，如果Thread不被销毁，Map里面的东西也无法被回收，会占用非常大的空间, 可能最终导致内存溢出。

要做的事情，也很简单，对于每个ThreadLocal的使用，都及时调用 remove() 清掉不需要的数据，强制释放内存。

