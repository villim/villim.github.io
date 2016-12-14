---
title: Color Console Output
layout: post
---

做输出版本号的功能。想着除了WEB端，命令行里面也能看到就更方便一点。不过黑压压的一片日志，完全看不清楚了。联想到Spring在命令行那个靓丽的LOGO，可以做做类似的东西。

简单的说，可以使用 [ANSI escape code](https://en.wikipedia.org/wiki/ANSI_escape_code),参考一下这个WIKI就行了。不过字符编码什么，永远都是挺麻烦的，参考也挺累的，知道怎么用也行。

![Colored Console Output](http://villim.github.io/img/2016/color-console-output.png)

```
public static final String ANSI_RESET = "\u001B[0m";
public static final String ANSI_BLACK = "\u001B[30m";
public static final String ANSI_RED = "\u001B[31m";
public static final String ANSI_GREEN = "\u001B[32m";
public static final String ANSI_YELLOW = "\u001B[33m";
public static final String ANSI_BLUE = "\u001B[34m";
public static final String ANSI_PURPLE = "\u001B[35m";
public static final String ANSI_CYAN = "\u001B[36m";
public static final String ANSI_WHITE = "\u001B[37m";


 private void showVersion() {
        System.out.println(ANSI_RED + "====================" + ANSI_RESET);
        System.out.println(ANSI_GREEN + " VERSION: " + env.getProperty("git.build.version", "") + ANSI_RESET);
        System.out.println(ANSI_GREEN + "REVISION: " + env.getProperty("git.commit.id", "") + ANSI_RESET);
        System.out.println(ANSI_RED + "====================" + ANSI_RESET);
    }
```