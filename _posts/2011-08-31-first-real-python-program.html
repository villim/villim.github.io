---
layout: post
title: First real Python Program
categories:
- PYTHON
tags:
- python
- Thread
status: publish
type: post
published: true
meta:
  _edit_last: '1'
author:
  login: villim
  email: villim@126.com
  display_name: Villim
  first_name: Villim
  last_name: Wong
---
<p>Python 上手还真的是很快，虽然偶尔看到一些关于 Python 的文章，但是真要说写个像样能用的东西，这是好像这是第一次在工作里用。东西很简单，留个纪念 ^_^。</p>
<p>本来的代码，是要做系统里的多线程并发的性能测试。 不方便贴出来，这里把它改成简单的并发 Telnet 测试。（结构没啥变化，不过代码看起来有点怪怪的了）</p>
<p><strong>MutiThreadPerformaceTest.py</strong></p>
<pre class="brush:py">import telnetlib
import threading
import sys

host = 'xxx.xxx.xxx.xxx'
port = 25

maxloopnum = 10
threadNumber = 10

def connect(host, port):
  for i in range(0,maxloopnum):
    try:
      print "--- start connect ---"
      tn = telnetlib.Telnet(host,port)

      tn.read_until("220 zimbra.linkers.local ESMTP Postfix") # Depends on your situation
      print "--- already connected, quit right now ---"
      tn.write("quit" + "\n")

    except:
      s=sys.exc_info()
      print "^^^ Encounter error ^^^ '%s' happened on line %d" % (s[1],s[2].tb_lineno)

class ThreadClass(threading.Thread):
  def run(self):
    connect(host,port)

for i in range(threadNumber):
  t = ThreadClass()
  t.start()</pre>
<p>&nbsp;</p>
<p>&nbsp;</p>
