---
title: Linux Skills (1)
layout: post
---

## 当前的外部IP地址

```bash
# curl ifconfig.me
```

## 使用参数 Max Depth

很多命令都提供 Max Depth 座位参数，用好了，可以大大提高效率。比如：

```bash
# sudo du -h --max-depth=1 /tmp
```

and

```bash
# sudo find /tmp -maxdepth 1 -user deploy -exec rm -rf {} \;
```

## 根据端口查询进程或服务

lsof 不仅可以看到端口情况，还可以看到服务的名字和PID，比价强大：

```bash
# lsof -iTCP:8080 -sTCP:LISTEN
# lsof -i:8080 
```

但lsof只能检查本机服务，如果只是检查端口状态，可以使用nmap：

```bash
nmap -sT   <DB-Domain> -p 1521
nmap -sT   localhost  -p 7676,8080,8090,8070
```

## 快速创建 Maven 子项目结构

```bash
# mkdir -p <maven-project-name>/src/{main/{java,resources},test/{java,resources}}
```

## 用 dig 代替 nslookup

比起nslookup， dig 能显示更详细的信息，比较一下结果：

```bash
➜  # nslookup villim.github.com
Server:		10.109.2.37
Address:	10.109.2.37#53

Non-authoritative answer:
villim.github.com	canonical name = github.map.fastly.net.
Name:	github.map.fastly.net
Address: 151.101.72.133
```

```bash
➜  # dig villim.github.com

; <<>> DiG 9.9.7-P3 <<>> villim.github.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 53310
;; flags: qr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4000
;; QUESTION SECTION:
;villim.github.com.		IN	A

;; ANSWER SECTION:
villim.github.com.	30	IN	CNAME	github.map.fastly.net.
github.map.fastly.net.	20	IN	A	151.101.72.133

;; Query time: 295 msec
;; SERVER: 10.109.2.37#53(10.109.2.37)
;; WHEN: Thu Nov 16 17:30:21 CST 2017
;; MSG SIZE  rcvd: 97
```