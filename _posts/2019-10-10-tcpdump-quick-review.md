---
title: Tcpdump Quick Review 
layout: post
---

As long as you still coding, sooner or later you will encounter network packages transfer issue. At that moment, the most powerful tool you can trust is **Tcpdump**. And you have another GUI friend **Wireshak** to make anylize easier.

![Tcpdump Logo](http://villim.github.io/img/2019/tcpdump-logo.jpg)

**Tcpdump** able to catch the packages sending on Internet, to understand what is the package? how it works? Ofcourse you need basic knowledge with TCP/IP protocol. 

## Tcpdump Parameters

After checking its manual, you should find how complex it is. Here just simplified for frequently-used ones.

* -i : specify which interface (network card) to listen. [ -i any ] means all.
* -S : Print absolute, rather than relative, TCP sequence numbers.
* -v，-vv，-vvv : more detailed print, even more, even more.
* -c number : continue capturing packets until the [number] package, then stop.
* -n : don't convert addresses to names
* -w : Write the raw packets to file rather than parsing and printing them out.  
* -A : Print each packet in ASCII.  Handy for capturing web pages. Do not use with [-X].
* -X : print the data of each packet in Hex and ASCII.
* -D : print the list of the network interfaces available on the system

## 1. List All Interfaces

```
➜  ~ tcpdump -D
1.en0 [Up, Running]
2.bridge0 [Up, Running]
3.p2p0 [Up, Running]
... ...
15.stf0
16.XHC20
```

another way is using **ifconfig** , which will give more detailed information.


## 2. Capture Packets from Specific Interface

```
➜  ~ tcpdump -i en0
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
listening on en0, link-type EN10MB (Ethernet), capture size 262144 bytes
23:46:29.415520 IP cnvpn.activenetwork.cn.https > wd00030376.active.local.63837: Flags [P.], seq 1005499679:1005499928, ack 3241751084, win 65535, length 249
23:46:29.415590 IP wd00030376.active.local.63837 > cnvpn.activenetwork.cn.https: Flags [.], ack 249, win 65535, length 0
23:46:29.417737 IP cnvpn.activenetwork.cn.https > wd00030376.active.local.63837: Flags [P.], seq 249:466, ack 1, win 65535, length 217

... ...

```

we can use these Parameters mentioned at beginning.

**Capture Only N Number of Packets**

using -c option, we can capture specified number of packets. then stop.

```
➜  ~ tcpdump -i en0 -c 2
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
listening on en0, link-type EN10MB (Ethernet), capture size 262144 bytes
23:50:44.395154 IP cnvpn.activenetwork.cn.https > wd00030376.active.local.63837: Flags [.], ack 3242972402, win 65535, length 0
23:50:44.423278 IP cnvpn.activenetwork.cn.https > wd00030376.active.local.63837: Flags [.], ack 118, win 65535, length 0
2 packets captured
2 packets received by filter
0 packets dropped by kernel
```

**Display Captured Packets in HEX and ASCII**

```
➜  ~ tcpdump -i en0 -c 2 -XX
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
listening on en0, link-type EN10MB (Ethernet), capture size 262144 bytes
23:58:21.676345 IP cnvpn.activenetwork.cn.https > wd00030376.active.local.63837: Flags [P.], seq 1026016629:1026016878, ack 3244839280, win 65535, length 249
	0x0000:  6c40 088e a446 6248 a570 7fe0 0800 4500  l@...FbH.p....E.
	0x0010:  0121 9141 4000 3206 9f4a d24a 8356 c0a8  .!.A@.2..J.J.V..
	0x0020:  0102 01bb f95d 3d27 c575 c168 5170 5018  .....]='.u.hQpP.
	0x0030:  ffff e514 0000 1703 0300 f400 ab86 1ef6  ................
	0x0040:  4940 63a1 894b 16f8 3af6 dd17 c3ff b268  I@c..K..:......h
	0x0050:  12b3 a1ad f047 debd 2480 d923 a25b 9d6a  .....G..$..#.[.j
	0x0060:  6922 f8db 4bc5 0a54 e0d9 3b70 4e6a 1e11  i"..K..T..;pNj..
	0x0070:  ab5d 87ad 4909 487f 95e6 8e6f 2e20 a8a7  .]..I.H....o....
	0x0080:  ba38 5ee4 90b0 0d0e 6bbf 2769 7337 0c71  .8^.....k.'is7.q
	0x0090:  f34e 03b7 b63b 0c51 6508 b40c 5521 f90b  .N...;.Qe...U!..
	0x00a0:  cfc9 f3c1 5967 eadc 657a 74ed e165 7bf7  ....Yg..ezt..e{.
	0x00b0:  9fbf 73ee 5db3 19c9 51b7 5df3 769e fa6e  ..s.]...Q.].v..n
	0x00c0:  34df 6d05 c867 f5eb 7d2f 55e2 f4aa ba56  4.m..g..}/U....V
	0x00d0:  cf93 47f3 208d 431b c6de 79b9 3883 3cb1  ..G...C...y.8.<.
	0x00e0:  5a19 c2bd 1cef abb4 3440 428f 92c3 23d8  Z.......4@B...#.
	0x00f0:  0802 6f06 0603 d5ec c229 4f64 53ca 0d0e  ..o......)OdS...
	0x0100:  583a 0d15 42f6 f61c f04a 2fab cfa2 ff41  X:..B....J/....A
	0x0110:  d2aa c448 ff6d 62e7 2728 1fe1 8816 72bc  ...H.mb.'(....r.
	0x0120:  3d1b e4ec e015 230a 27a3 124e 1365 30    =.....#.'..N.e0
23:58:21.676527 IP wd00030376.active.local.63837 > cnvpn.activenetwork.cn.https: Flags [.], ack 249, win 65535, length 0
	0x0000:  6248 a570 7fe0 6c40 088e a446 0800 4500  bH.p..l@...F..E.
	0x0010:  0028 0000 4000 4006 2385 c0a8 0102 d24a  .(..@.@.#......J
	0x0020:  8356 f95d 01bb c168 51e5 3d27 c66e 5010  .V.]...hQ.='.nP.
	0x0030:  ffff 868c 0000                           ......
2 packets captured
2 packets received by filter
0 packets dropped by kernel
```

## 3. Capture and Save Packets in a File

```
➜  ~ tcpdump -i en0 -w ~/Downloads/test.pcap
tcpdump: listening on en0, link-type EN10MB (Ethernet), capture size 262144 bytes
^C856 packets captured
943 packets received by filter
0 packets dropped by kernel
```

**Every 60 seconds save to a file, named with timestamp with root user file modes.**

```
➜  ~ tcpdump -i en0 -G 60 -Z root -w %Y_%m%d_%H%M_%S.pcap
```


## 4. Read Captured Packets File

```
➜  ~ tcpdump -r ~/Downloads/test.pcap
reading from file /Users/williamwang/Downloads/test.pcap, link-type EN10MB (Ethernet)
00:01:31.775719 IP cnvpn.activenetwork.cn.https > wd00030376.active.local.63837: Flags [P.], seq 1030845639:1030845872, ack 3245488491, win 65535, length 233
00:01:31.775808 IP wd00030376.active.local.63837 > cnvpn.activenetwork.cn.https: Flags [.], ack 233, win 65535, length 0
```

## 5.  Capture IP address Packets

Show IP ranther than domain names

```
➜  ~ tcpdump -i en0  -n
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
listening on en0, link-type EN10MB (Ethernet), capture size 262144 bytes
00:07:00.375221 IP 210.74.131.86.443 > 192.168.1.2.63837: Flags [P.], seq 1035766394:1035766611, ack 3246731075, win 65535, length 217
00:07:00.375326 IP 192.168.1.2.63837 > 210.74.131.86.443: Flags [.], ack 217, win 65535, length 0

```

## 6. Capture only TCP|IP|ARP|UDP Packets.

```
➜  ~ tcpdump -i en0 [tcp|udp|ip|arp] -n
```

## 7. Capture Packet from Specific Port

```
➜  ~ tcpdump -i en0 tcp -n port 22
```

## 8. Capture Packets from source IP

```
➜  ~ tcpdump -i en0 src xxx.xxx.xxx.xxx
```

## 9. Capture Packets from destination IP

```
➜  ~ tcpdump -i en0 dst xxx.xxx.xxx.xxx
```

## 10. Capture Packets from whole network section

```
➜  ~ tcpdump src host 10.126.1.222 and dst net 10.126.1.0/24
```


About Wireshark, just open pcap file with it. It's quite simple and direct, but to have better understanding, that's another story.