---
title: Big O Notation
layout: post
---

## What is Big O Notation

When we discussing Programming Algorithm, we will use BIG O NOTATION. 

### Here's a quick understading

* It's written as: O(1), O(n), O(n^2), O(nlog n) ...
* The Logarithm **log** in Big-O-Notation, means **log with base 2**
* Big-O-Notation doesn't know concrete time cost, thus there's no UNIT for it, e.g. seconds, hours
* Big-O-Notation only shows the time cost trends when data growing

## 5 Most Common Algorithm

Here's 5 most common algorithm that listing as order from fast to slow :

![diagram for 5 common algorithm](http://villim.github.io/img/2017/big-o-notation-5-common-algorithm.jpg)

1. O(log n) Logarithmic time, such as binary search
2. O(n) Linear time, such as simple search
3. O(n * log n) such as Quick Sort
4. O(n2) such as Select sort
5. O(n!) such as Traveller problem



## Basic Logarithm

To have better understanding for Big O Notation, we need understand Logarithm.

### Definition

![Logarithm Definition](http://villim.github.io/img/2017/big-o-notation-logarithm-definition.jpg)

### Logrithm Properties

![Logarithm Properties](http://villim.github.io/img/2017/big-o-notation-logarithm-properties.png)


**Important note:**

* the bases of all logarithms in the expression must be the same.
* the arguments of the logarithms must be positive and the bases of the logarithms must be positive and not equal to 1  in order for this property to hold!