---
layout: post
title: Practical GREP
---

Normally we just using GREP in following way:

```bash
# grep 'ERROR' /var/log/project.log
# cat project.log | grep 'ERROR'
```
That's ok, but usually we do need more in real work.

Let's say, 

### We want to count ERROR in log file:

```bash
# grep 'ERROR' /var/log/project.log | wc -l
# grep -c 'ERROR' /var/log/project.log 
```
We were trying to search word ERROR, but infact previous command can retrieve lines contains  ERROR, that means if there are words ERROR1, ERROR2, ERROR3 ... They also counted, that's not we want.

### So we need search by word:

```bash
# grep -w 'ERROR' /var/log/project.log
```
Of course we are able to search word start with ERROR or end with ERROR too:

```bash
# grep -w '<ERROR' /var/log/project.log
# grep -w 'ERROR\>' /var/log/project.log
```

Locate the line where contains ERROR, that's great!! but I'm not able to see the error details, so I need see the lines AHEAD and BELOW too. Let's say,

### Check 10 lines around matched search criteral

```bash
# grep -C 10 'ERROR' /var/log/project.log
```
I can just view the lines Ahead or Below for sure:

```bash
# grep -A 10 'ERROR' /var/log/project.log  # ahead
# grep -B 10 'ERROR' /var/log/project.log  # below
```

And Don't forget 

#### we can use RegExpression too. 

If I want to check the Thread-1 to Thread-8, I can do :

```bash
# grep 'Thread-[1-8]' /var/log/project.log
```
### we can also use extended regexp

like locate IP address:

```bash
# grep -E '\b[0-9]{1,3}(\.[0-9]{1,3}){3}\b' /var/log/project.log
```

Another senario is when you working with folder, there may a lot of different file types: .java, .xml, .properties, .conf ...

we may need do
### Regression Grep
```bash
#  grep -rl 'SOMETHING' .
```

But my maven project, I just need find things in pom.xml. The quickest way is to 

### Integrate with FIND

```bash
#  find ~/project-dir -name pom.xml -exec grep 'SOMETHING' {} +
```