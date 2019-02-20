---
title: weather forecast in command line
layout: post
---

## WTTR.IN

Check weather is what we may need from time to time, it's a quite usefully feature. 

Now we can do it even in command line! even without leave our Terminal ~ That's really great! What we need is just **CURL**

```bash
$ curl wttr.in
```

![wttr.in](http://villim.github.io/img/2019/weather-in-command.png)

Though it's simple enough, however seems still too many characters and not catchable. Let's make it more meaningful.

Let's use Alias to customise our own command.

## Alias

with **alias** we can see all the current defined commands:

```bash
$ alias
```

## Temporary Aliases

and create an Alias is also easy, just like:

```bash
$ alias weather="curl wttr.in"
```

After it's done, we can just check weather with:

```bash
$ weather
```

But wait, after we close Terminal, **weather** not working any more. Cause it's temperary, what we need is a pernamnent one.

## Permanent Aliases

Different Shell need change different file, like:
 
* Bash – ~/.bashrc
* ZSH – ~/.zshrc

I'm using ZSH, so we going to do following:

```bash
$ vim ~/.zshrc  ## add one line ' alias weather="curl wttr.in" '
$ source ~/.bashrc
```