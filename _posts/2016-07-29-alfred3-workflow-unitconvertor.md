---
title: Alfred3 Convertor Workflow
layout: post
---

## Gab
The way Chinese discribe thing is really different with English speaking countries.

Take how to describe Address for example. Chinese would start from the biggest to detailed, like 'China, Sichuan, Chengdu, xxx Road, No.3 Section, #123'. However, in English it will be '#123, No.3 Section, xxx Road, Chengdu, Sichuan, China'.

When it comes to Numbers, we also see this different. "3/4" in Chinese, we say **4分之3**, which means the denominator (4) first then numerator (3). But in English, we say **Three Quarters**, which is numerator (3) first.

Besides that, the most exotic Americans, even make the understanding worse. Everyone is using Kilemeters as unit, they prefer Miles. And when chating with them, it's always confused me with temperature, cause they are talking with Fahrenheit  -_-||


## Alfred3 

Thinking about converting such kinds of things, Alfred is a great tool. It's direct, and quick!! Have been using it for quite a long time, this is a good chance to create a small tool by myself.

Researching for a while, it's quite easy for what I want, let's see the final result first. It looks like this:

![Temperature Convertor Demo](http://villim.github.io/img/2016/alfred3-workflow-unit-convertor-demo-temperature.png)

I only added temperature converting between Fathenheit and Celsius. And between Kilemeters and Miles at this moment.

![Unit Convertor Inside](http://villim.github.io/img/2016/alfred3-workflow-unit-convertor-inside.png)

To implement this requirement, just need 4 **Script Filter** and a very simple script. But it do cost me quite some time to make it clear how to generate result XML. 

The source code is here [alfred3-workflow-unit-convertor](https://github.com/villim/alfred3-workflow-unit-convertor)








