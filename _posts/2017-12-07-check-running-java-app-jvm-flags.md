---
title: Check Running Java App's JVM Flags
layout: post
---

Usually we just setting all kinds of JVM parameters in conf file, and left it there, but when we need optimize JVM, we will have the demand to see whether a running App is working as we configured.


## A Simple Java Application

Here's a sample Java application. When running it, use the JVM parameters in comment. 

```java

/**
 * -Xmx20m -Xms20m -Xmn10m -XX:+UseParNewGC  -XX:+UseConcMarkSweepGC
 * -XX:+UseCMSInitiatingOccupancyOnly  -XX:CMSInitiatingOccupancyFraction=75
 * -XX:+PrintGCDetails -XX:+PrintGCDateStamps -XX:+PrintHeapAtGC
 */
public class JVM {

    private static final int _1MB = 1024 * 1024;

    public static void main(String[] args) throws Exception {

        byte[] b1 = new byte[2 * _1MB];
        byte[] b2 = new byte[2 * _1MB];
        byte[] b3 = new byte[2 * _1MB];
        byte[] b4 = new byte[4 * _1MB];
        System.in.read();
    }
}
``` 


## Check with command line

We can use JPS or JINFO, while JINFO will show much detailed information with all the parameters

### JPS - Java Virtual Machine Process Status Tool

* -m	Output the arguments passed to the main method. The output may be null for embedded JVMs.
* -l	Output  the  full  package name for the application's main class or the full path name to the application's JAR file.
* -v	Output the arguments passed to the JVM.


```bash
➜  ~ jps -lvm
91587 JVM -Xmx20m -Xms20m -Xmn10m -XX:+UseParNewGC -XX:+UseConcMarkSweepGC -XX:+UseCMSInitiatingOccupancyOnly -XX:CMSInitiatingOccupancyFraction=75 -XX:+PrintGCDetails -XX:+PrintGCDateStamps -XX:+PrintHeapAtGC
```


### JINFO - configuration info

* -flags	prints command line flags as name, value pairs

```bash
➜  ~ jinfo -flags 91587
Attaching to process ID 91587, please wait...
Debugger attached successfully.
Server compiler detected.
JVM version is 25.45-b02
Non-default VM flags: -XX:CICompilerCount=4 -XX:CMSInitiatingOccupancyFraction=75 -XX:InitialHeapSize=20971520 -XX:MaxHeapSize=20971520 -XX:MaxNewSize=10485760 -XX:MaxTenuringThreshold=6 -XX:MinHeapDeltaBytes=196608 -XX:NewSize=10485760 -XX:OldPLABSize=16 -XX:OldSize=10485760 -XX:+PrintGCDateStamps -XX:+PrintGCDetails -XX:+PrintHeapAtGC -XX:+UseCMSInitiatingOccupancyOnly -XX:+UseCompressedClassPointers -XX:+UseCompressedOops -XX:+UseConcMarkSweepGC -XX:+UseFastUnorderedTimeStamps -XX:+UseParNewGC
Command line:  -Xmx20m -Xms20m -Xmn10m -XX:+UseParNewGC -XX:+UseConcMarkSweepGC -XX:+UseCMSInitiatingOccupancyOnly -XX:CMSInitiatingOccupancyFraction=75 -XX:+PrintGCDetails -XX:+PrintGCDateStamps -XX:+PrintHeapAtGC
```


## Check in Java Code

```java
import java.lang.management.ManagementFactory;
import java.lang.management.RuntimeMXBean;
...

// get a RuntimeMXBean reference
RuntimeMXBean runtimeMxBean = ManagementFactory.getRuntimeMXBean();

// get the jvm's input arguments as a list of strings
List<String> arguments = runtimeMxBean.getInputArguments();
```

