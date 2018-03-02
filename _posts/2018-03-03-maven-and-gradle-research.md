---
title: Maven & Gradle Research
layout: post
---

## What is Maven & Gradle

Apache Maven is a software project management and comprehension tool. Based on the concept of a project object model (POM), Maven can manage a project's build, reporting and documentation from a central piece of information.

[Maven](http://maven.apache.org/) started from 2002, Maven1 rapidly replaced **Ant**. And later Maven even refactored itsself, from Maven1 to Maven2. And Maven2 have becoming standard for more than 10 years.


Gradle is an open source build automation system that builds upon the concepts of Apache Ant and Apache Maven and introduces a Groovy-based domain-specific language (DSL) instead of the XML form used by Apache Maven of declaring the project configuration. 

[Gradle](https://gradle.org/) started around 2012, now seems like a new supper star. First impression is, it cater to the current prevalent idea, configuration is code. Developers hate XML, as we trying to use annocation replace XML in Spring, Gradle is also trying to get rid of XML.


## Major Features

In a word, they are both **Project Management Tool**. As Maven have became a dominate standard,  it provides following features: 

* dependencies management
* module management
* consistent project structure
* consistent building process
* plugin management

We can compare with Gradle in these aspects.

### Dependencies Management

Maven use groupId, artifactId, version to identify a dependency.

```xml
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.12</version>
    <scope>test</scope>
</dependency>
```

Gradle learned this depency management from Maven, but rather than xml based configuration, simply it  with groovy like style.

```
dependencies {
    compile 'org.hibernate:hibernate-core:3.6.7.Final'
    testCompile ‘junit:junit:4.+'
}
```

Maven provide 6 scopes: compile, provided, runtime, test, system, import.

Gradle has only 4 scopes: compile, runtime, testCompile, testRuntime. But we can create own code to implement the missing scope, for example [provided] scope.

Gradle only 4 scopes: compile、runtime、testCompile、testRuntime. But we can create own code to implement provided scope.  [How to use provided scope in Gradle](https://stackoverflow.com/questions/18738888/how-to-use-provided-scope-for-jar-file-in-gradle-build)

But Gradle able to support dynamic version dependency with "+".

And Gradle solve dependencies version conflict better, which was really a huge issue in Maven. Check [Gradle Dependency Management](https://docs.gradle.org/current/userguide/introduction_dependency_management.html)

### Modules Management

Usually one project contains multiple sub modules.

Maven must have a PARENT POM and all sub-modules will inherit from PARENT, so if we want special configuration for some of these modules, we need define them in each modules, that could bring repeat codes.

While Gradle could define a configuration is gloable or just for some modules by **allprojects** or **subprojects**. So Gradle should be able to provide a much clear and consistent code, should be better to support Multi Modules configuration. 

### Building Phrases

Maven's building follows this order:

```xml
<phases>
  <phase>validate</phase>
  <phase>initialize</phase>
  <phase>generate-sources</phase>
  <phase>process-sources</phase>
  <phase>generate-resources</phase>
  <phase>process-resources</phase>
  <phase>compile</phase>
  <phase>process-classes</phase>
  <phase>generate-test-sources</phase>
  <phase>process-test-sources</phase>
  <phase>generate-test-resources</phase>
  <phase>process-test-resources</phase>
  <phase>test-compile</phase>
  <phase>process-test-classes</phase>
  <phase>test</phase>
  <phase>prepare-package</phase>
  <phase>package</phase>
  <phase>pre-integration-test</phase>
  <phase>integration-test</phase>
  <phase>post-integration-test</phase>
  <phase>verify</phase>
  <phase>install</phase>
  <phase>deploy</phase>
</phases>
``` 

This is a fixed workflow, we can’t change. Any maven plugin have to defined which phrase it should be.  That’s the reason Maven is a little bit slow. and some times , we can’t clearly define a plugin should go which phrase.

Gradle is totally different, Gradle itself is decoupled with building phrased. To do sth, just need create a TASK and this one depends on existed TASKs.  It’s means you have to build your own building phrases.

### Project Structure 

No real difference

###  Plugin Management

Maven probably have more stable plugins. 

### Performance 

From Gradle's [official document, which](https://gradle.org/maven-vs-gradle/) compare to Maven. We can see Gradle is much faster than Maven. However, I doubt if the testing is fair. Even it's true, still need based performance on reliability.


## My Conclusion

Maven vs Gradle, seems like we discussing about Java vs Python. 

Maven and Java are both verbose, making code quite redundant, but they have clear and consistent definition for concepts, that once you understand, won't make stupid mistake. That's why Java is suitable for big project which has a big development team that with different experienced programmer.
 
However, Maven is like a fixed box, you are not allowed to be too innovative to jump out the box.  We have to use what it provided.

In the other hand, Gradle give you more power, you are not locked in the box, you have to build the Box, and you can create whatever as you like. That also mean, developers may create a monster that no one understand at all.

XML is verbose, but it's easy to understand even for a freshman. So even you never use Maven before, you can still understand with these tags.

As a contrast, Groovy configuraiton is compact, but hard to undertand unless you are familiar with it.  Some times, inconvenient is also a advantage.

Finally, choose any one of them is ok, there's no best tool at all, who is using them decide what can tool do. 

## Gradle like Maven

But the way, if just want get rid of XML configuration, make configuration compact,  there’s project, that allow using Maven in Gradle’s groovy way : [GitHub - takari/polyglot-maven](https://github.com/takari/polyglot-maven)