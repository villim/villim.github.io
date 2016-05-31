---
title: Vim Substitute and Global
layout: post
---

Wanted to modify a xml file, there were some scenarios I need to modify or delete lines based on regular expression for multiple lines. After tried for a while I almost believe I need create a python or shell script to do it. Then I found Global commands, really powerful. And with advanced substitute command, it can complete my requirement perfectly!

## VERY MAGIC & NOMAGIC

### very magic : search as regular

Vim's regular expression syntax is more like POSIX. So when I need match a date like "2016-06-01", the regular is 


```bash
\d\{4\}-\d\{2\}-\d\{2\}/
```

Have to use quite many excape characters. After using **VERY MAGIC**

```
\v (lowercase) : 

all the other charecters have special meaning except **_**, **-**, **0-9** and **a-zA-Z**

```

So using VERY MAGIC, it will be much more readable.

```bash
\v\d{4}-\d{2}-\d{2}
```

### very nomagic : search as literal meaning

```
\V (uppercase) : 

all the characters has their literal meaning and must use \ for escape meanning.
```


## Advance Subsitute
### Special Character in Replace Field

The subsitute format is like:

```
:[range]s[ubstitute]/{pattern}/{replace-string}/{flags}
```

We can use following special characters in replace-string:
* \r is newline, \n is a null byte (0x00).
* \& is ampersand (& is the text that matches the search pattern).
* \0 inserts the text matched by the entire pattern
* \1 inserts the text of the first backreference. \2 inserts the second backreference, and so on.

### Search with Capatured Group

Inorder to use **\1** to **\N**, we need use **()** in search field to set matched text into groups.

Still using previous example,  to match "2016-06-01", the regular can be written as

```bash
\v(\d{4})-(\d{2})-(\d{2})
```

In this way, I can use \1 refer to 2016, \2 refer to 06 and \3 refer to 01.


### Substitute Example

I want to change the date to datetime format in xml for all 

```
<sch:sellThroughDate>2016-06-01</sch:sellThroughDate> 
```

The command could be:

```bash
:%s/sellThroughDate>\v\d{4}-\d{2}-\d{2}/\0T00:00:00/g
```


## Global Command

The syntax is :

```
:[range]g/{pattern}/{cmd}
```

Gloabal act Ex command on multiple lines, that means you can almost do anything beyond your imagination.

### Gloabal Delete

The easiest one I were using is delete lines based on a pattern

```
:g/{pattern}/d
```

We can also delete all the lines unmatch with:

```
:v[group]/{pattern}/d
```

### Gloabal Sort
This is a command to sort element inside CSS, like :

```
html{
	margin: 0;
	padding: 0;
	border: 0;
	font-size: 100%;
	vertical-aligin: baseline;
}
```
You can run as:

```bash
:g/{/ .+1,/}/-1 sort
```




