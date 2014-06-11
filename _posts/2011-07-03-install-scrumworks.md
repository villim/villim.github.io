---
layout: post
title: Install ScrumWorks
categories:
- AGILE
tags:
- Agile
- ScrumWorks
- Ubuntu
status: publish
type: post
published: true
meta: {}
author:
  login: villim
  email: villim@126.com
  display_name: Villim
  first_name: Villim
  last_name: Wong
---
<p>因为做Innovation项目的原因，需要一个Scrum的管理工具。</p>
<p>公司使用的 VersionOne 当然是不错的选择，不过没有权限添加新的项目，所以考虑自己本地解决。Excel 本来是第一选择，无奈修改和共享真的太麻烦。Xplanner 大家都熟悉，而且免费，可确实不算好运。于是找到目前市场排行第三的 ScrumWorks，试用了一下，感觉很不错。有WEB界面，也有富客户端，比较VersionOne来说，简化的东西少了很多很多，但使用起来相当便捷，很好运。虽然软件本身收费，但是 小团队，可以申请到20多年的使用权限，那肯定是够用的了。</p>
<p>首先当然先要下载安装包：</p>
<p>到 <a title="scrumworks" href="http://www.open.collab.net/products/scrumworks/ " target="_blank">ScrumWorks官网</a> 可以找到 “<strong>Free 10-user ScrumWorks Pro</strong>”</p>
<p>页面跳转后，填入基本信息，确认Lisence，就可以看到下载页面。</p>
<p>安装文档写得很详细，按照 <a title="ScrumWorks Install Guide" href="http://danube.com/docs/scrumworks/pro/latest/readme.html" target="_blank">官方安装文档</a> 一步步做就好了。</p>
<p>需要注意的是需要提前准备好Mysql 的数据库，和一个数据库实例：</p>
<p>1. Connect to mysql:</p>
<pre class="brush:shell">mysql -u root -p</pre>
<p>2. Create xplanner database:</p>
<pre class="brush:shell">CREATE DATABASE scrumworks CHARACTER SET UTF8 COLLATE utf8_general_ci</pre>
<p>3. Create scrumworks user:</p>
<pre class="brush:shell">GRANT ALL PRIVILEGES ON scrumworks.* TO 'scrumworks'@'localhost' IDENTIFIED BY 'scrumworks' WITH GRANT OPTION;</pre>
<p>4. Exit out of mysql:</p>
<pre class="brush:shell">quit;</pre>
<p>安装完后，访问 http://localhost:8080/scrumworks/ 即可访问，注意初始管理员帐号密码是： administrator/password</p>
