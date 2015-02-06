---
layout: post
title: Max Socket Port Number
tags: Java

---

When creating Socket in Java, we have to specify PORT NUMBER. 

{% highlight java %}
Socket(InetAddress address, int port)
//Creates a stream socket and connects it to the specified port number at the specified IP address.
{% endhighlight %}

But, what's the maximum number of port ? Just find myself not clear about it.

From the interface, it seems clear, cause port is a INT. So that's 65535. 

Sockets have two major modes of operation: connection-oriented (TCP) and connectionless (UDP). 

After check TCP protocal we can know, port is an unsigned 16-bit integer, so again 65535.

One more thing, should know:
In range 1-1023 are the privileged ones. They are reservered for System. So applications will have to run as ROOT user to listen to these ports.
