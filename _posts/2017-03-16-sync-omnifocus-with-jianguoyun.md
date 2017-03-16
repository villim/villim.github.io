---
title: Sync OmniFocus with Jianguoyun
layout: post
---

OmniFocus is wounderful, but **Omni Sync Server** not ... many THANKS to THE GREAT WALL!

Lucky, OmniFocus support **WebDAV**, so we can choose a faster network cloud disk solution, like Box, Dropbox, Google Drive ...

But native privider will be better, as we know most of cloud disk providers have shut down their products ... many THANKS to WHOEVER! [Jianguoyun](https://www.jianguoyun.com/) I have been using for a while, it's really fast, although free space is quite small, but enough to sync Apps data.

## What is WebDAV

[WebDAV](https://en.wikipedia.org/wiki/WebDAV)) is short for **Web Distributed Authoring and Versioning**. It is an extension of the Hypertext Transfer Protocol (HTTP) that allows clients to perform remote Web content authoring operations.

Why we need WebDAV? 

* we can directly operate files throught HTTP
* we can easily encript everything
* It working like a remove network diskspace

## Steps to Setup Jinaguoyun

* Regist in [Jianguoyun](https://www.jianguoyun.com/d/signup)
* Third-party Applications Management
	1. Settings -> Security -> Add App auth
	2. Name is as Omnifocus, Will generate a Application Password
* Go Jianguoyun **Files**, create folder **omnifocus** under root fold


## Steps to configure OmniFocus

* Open OmniFocus -> Preference -> Synchronization
* Check **Advanced(WebDAV)**
* Address with: ```https://dav.jianguoyun.com/dav/omnifocus/```
* Fill in previous generated Application Password


