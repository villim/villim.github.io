---
title: Add toString() for JAXB classes
layout: post
---

When I want to see the toString from a auto generated JAXB class, just found there's no toString() at all.

You just need plugin for **maven-jaxb2-plugin**.
Here's my cofiguration:

{% highlight xml %}
    <build>
        <plugins>
            <plugin>
                <groupId>org.jvnet.jaxb2.maven2</groupId>
                <artifactId>maven-jaxb2-plugin</artifactId>
                <executions>
                    <execution>
                        <goals>
                            <goal>generate</goal>
                        </goals>
                    </execution>
                </executions>
                <configuration>
                    <accessExternalSchema>all</accessExternalSchema>
                    <extension>true</extension>
                    <args>
                        <arg>-XtoString</arg>
                        <arg>-XtoString-toStringStrategyClass=io.github.villim.MyToStringStrategy</arg>
                        <arg>-Xequals</arg>
                        <arg>-XhashCode</arg>
                    </args>
                    <plugins>
                        <plugin>
                            <groupId>org.jvnet.jaxb2_commons</groupId>
                            <artifactId>jaxb2-basics</artifactId>
                            <version>0.9.5</version>
                        </plugin>
                    </plugins>
                </configuration>
            </plugin>
        </plugins>
    </build>
{% endhighlight %}


The only problem is , the genrated toString() not readable at all. Luck, we can create our own toStringStrategy.
 
 
 
{% highlight java %}
 package io.github.villim;

import java.util.Arrays;

import org.jvnet.jaxb2_commons.lang.ToStringStrategy;
import org.jvnet.jaxb2_commons.locator.ObjectLocator;

public class MyToStringStrategy implements ToStringStrategy {

    @Override
    public StringBuilder append(final ObjectLocator objectLocator, final StringBuilder stringBuilder, final boolean fieldName) {
        return stringBuilder;
    }

   	... ...

    @Override
    public StringBuilder appendEnd(final ObjectLocator objectLocator, final Object object, final StringBuilder stringBuilder) {
        return stringBuilder.append(")");
    }

    @Override
    public StringBuilder appendField(final ObjectLocator objectLocator, final Object object, final String fieldName,
            final StringBuilder stringBuilder, final boolean value) {
        return appendField(stringBuilder, fieldName, value);
    }

    ... ...

    @Override
    public StringBuilder appendStart(final ObjectLocator objectLocator, final Object object, final StringBuilder stringBuilder) {
        first = true;
        return stringBuilder.append(object.getClass().getSimpleName()).append("(");
    }
}

{% endhighlight %}