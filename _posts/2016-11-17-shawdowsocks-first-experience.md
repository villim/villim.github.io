---
title: shadowsocks 初体验
layout: post
---

先上结论，就目前的体验来说，Shadowsocks (SS) 还是不能替代 VPN 的，因为要对不同的软件单独做设置，使用起来不是那么方便。比如在Terminal里面,多少还是会改变使用习惯，至少让我有隔应。对于普通用户来说，SS 足够好了。对于码代码的来说，应该是VPN非常棒的补充，毕竟它有最稳定的穿墙能力。

## 原理

看看这个 [不完全指南](http://www.auooo.com/2015/06/26/shadowsocks%EF%BC%88%E5%BD%B1%E6%A2%AD%EF%BC%89%E4%B8%8D%E5%AE%8C%E5%85%A8%E6%8C%87%E5%8D%97/) 就很清楚了。

![Shawdowsocks Workflow](shadowsocks-first-experience-01.png =346x160)

简单说一下，Shadowsocks是对SSH Tunnel的升级，把之前简单的端到端的协议拆分成了 ssh-client 和 ssh-server。因为和客户端通信的ssh-client在GFW之外，而ssh-server之间是加密通信，从而保证了消息里的特征码不能被GFW捕获，也就几乎不可能被封掉了。

## 使用

要使用SS，前提自然是有shadowsocks ssh-server了。可以购买，也可以自己租用VPS搭建。这里先假设已经有了一台, 我们需要以下信息：

```
server ip: xxxx-xxxx-xxxx-xxxx
server port : xxxx
encryption: aes-256-cfb | aes-128-cfb | xxxx
password: xxxx
```

### Shawdowsocks App

可以在[官网](https://shadowsocks.org/en/download/clients.html)看到所有的客户端软件。

在Mac上我们可以使用 ShadowsocksX-NG ，配置相当简单，到 Servers - Active Shawdowsocks -> Server Preference 里添加即可使用。

### Surge 

大受好评的 [Surge](http://nssurge.com/) 也可以做这个事情，据说 iOS 版本比 Mac 更好用，不过当然价格也是贵的不要不要的，iOS 要328¥，Single Mac License 还要 50$。当然人家是 Web Developer Tool and Proxy Utility，没人要你做这么简单的事情。可以试用30天，建议先尝试，仅针对姿势修正的功能来说，优点在于可以收工更准确配置Proxy策略，支持更多协议，如果有SSH Tunnel也可使用。我感觉还不错，只是价格太贵，以目前人气，估计短时间不会降价的。不过对折时一定要来一发。

使用Surge的确是麻烦一点的。当然也可以简单的来，先搜索别人共享的配置文件，加载后即可。

### Proxychains

设置好后，浏览器是能正常工作的，其他的App需要单独设置。比如Terminal 也需要代理，会麻烦一点了。

#### Proxychains 安装

```
brew install proxychains-ng
```

编辑proxychains配置文件：
```
vim /usr/local/etc/proxychains.conf
```
最后的配置如下：

```
111 [ProxyList]
112 # add proxy here ...
113 # meanwile
114 # defaults set to "tor"
115 #socks4         127.0.0.1 9050
116 socks5  127.0.0.1 1086
```

#### Proxychains 使用

正常使用需要加上 proxychains4 命令：

```
proxychains4 git pull origin master
```
不仅不好用，还破坏了命令补全的功能，网上有个好办法。首先用短别名替换 proxychains4。

```
vim ~/.zshrc 
```
添加 
```
alias pc='proxychains4'
```
然后到iTerm里 **iTerm -> Preferences -> Profiles -> Keys** 
，新建一个快捷键:

* 例如 ⌥+↩︎ ，
* Action 选择 Send Hex Code，
* 键值为 0x1 0x70 0x63 0x20 0xd，
* 保存生效。

现在就可以像之前使用 Git 一样使用，只是，最后不能直接 ↩︎，而需要用 ⌥+↩︎ 。















