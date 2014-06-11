---
layout: post
title: Uncover LDAP
categories:
- LINUX
tags:
- LDAP
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
<p>Already knowing about LDAP for some years, but never really understand it. This week, I spent some time to get more familiar with it, there's more stuff than expected to really  master it. So, I just record some simple and plain understanding here at first.</p>
<h4><span style="color: #008000;">What is <strong>LDAP</strong> short for ?</span></h4>
<p><strong>LDAP</strong> means <strong>L</strong>ightweight <strong>D</strong>irectory <strong>A</strong>ccess <strong>P</strong>rotocol.  So it's just a LIGHTWEIGHT <strong>DAP</strong>, then new question would be :</p>
<h4><span style="color: #008000;">What is <strong>DAP</strong> ?</span></h4>
<p>In the earlier 1970s, there's a requirement for Telecommunication companies to produce and manage telephone directories. So X.500 Directory is introduced, X.500 directory services were traditionally accessed via the X.500 Directory Access Protocol, which required <strong>O</strong>pen <strong>S</strong>ystems <strong>I</strong>nterconnection protocol stack (OSI protocol).</p>
<p>We can just think DAP as a phone yellow book. where contains all the entries with telephone number, person names and address that we may look for.</p>
<h4><span style="color: #008000;">So why LDAP is a Lightweight DAP?</span></h4>
<p>we know INTRANET or later INTERNET was started from around 1974, and they also need a way to use DAP. However, internet is build on TCP/IP protocol, not OSI protocol. Thus LDAP comes, it was build to using TCP/IP to access DAP at the beginning. And LDAP becomes more and more popular in the later days, thus we are mostly referring LDAP to DAP now. But there's no LDAP directory, only DAP directory. We can think LDAP as a way to access DAP.</p>
<h4><span style="color: #008000;">The Usage of LDAP</span></h4>
<p>As a directory service, it must be very convenient and quick to look for some thing.  Just like,</p>
<p><em>"Search in the company email directory for all people located in Boston whose name contains 'Jesse' that have an email address. Please return their full name, email, title, and description."</em></p>
<p>This could also be a main reason, a common usage of LDAP is to provide a "single sign-on" function. That means one password for a user is shared between many services, such as applying a company login code to web pages , so that staff log in only once to company computers, and then are automatically logged into the company intranet.</p>
<h4><span style="color: #008000;">Structure of LDAP</span></h4>
<p>although the structure of LDAP seems relatively complex, it is fairly simple to understand. There's just Entry and Attribute in it.</p>
<ul>
<li>An <strong>entry</strong> consists of a set of attributes</li>
<li>An <strong>attribute</strong> has a name (an attribute type or attribute description) and one or more values. The attributes are defined in a <strong>schema</strong>.</li>
<li>Each attribute has  a unique identifier : it's <strong>Distinguished Name (DN)</strong>. This consists of its <strong>Relative Distinguished Name (RDN)</strong>, constructed from some attribute(s) in the entry.</li>
</ul>
<p><span style="color: #808080;">** <em>Think of DN as the full file path and RDN as relative filename (e.g. /var/tmp/myfile.txt is DN, myfile.txt is RDN)</em></span></p>
<p><em>Let's see a example data:</em></p>
<pre class="brush:plain"> dn: cn=John Doe,ou=people,dc=example,dc=com
 cn: John Doe
 givenName: John
 sn: Doe
 telephoneNumber: +1 888 555 6789
 telephoneNumber: +1 888 555 1232
 mail: john@example.com
 manager: cn=Barbara Doe,dc=example,dc=com
 objectClass: inetOrgPerson
 objectClass: organizationalPerson
 objectClass: person
 objectClass: top</pre>
<p>The <strong>dn</strong> just like a primary key, <strong>cn</strong>,<strong> givenName</strong>,<strong> sn, telephoneNumber</strong>,<strong> mail</strong>,<strong> manager </strong>are attributes. These attributes are defined in objectClass, like <strong>inetOrgPerson</strong>, <strong>organizationalPerson</strong>, <strong>person</strong>, <strong>top</strong>. These objectClass are referring to their schemas.</p>
<p>Here, the DN is "cn=John Doe, ou=people,dc=example, dc=com". what's <em><strong>ou=people,</strong><strong>dc=example, dc=com </strong>? </em>LDAP is directory, in nowadays we usually organise directory by DNS name. so the directory tree is like following:</p>
<pre>        dc=com
            |
        dc=example
       /          \
 ou=people     ou=groups
  /
cn=John Doe</pre>
<p>dc means <strong>Domain Component</strong>. In fact, this DN is not good enough. we say DN is distinguished Name, but the name "John Doe" may encounter a lot of duplication of names. Usually in real situation we use <strong>uid </strong>as the key, so DN is some thing like "uid=123456, ou=people,dc=example, dc=com".</p>
<p>&nbsp;</p>
<h4><span style="color: #008000;">Operations on LDAP</span></h4>
<p>there are  a plethora of operations that can be performed on the LDAP</p>
<ul>
<li><strong>Add</strong> - Used to insert a new entry into the directory-to-server database. If the name entered by a user already existed, the server fails to add a duplicate entry and instead shows an "entryAlreadyExists" message.</li>
<li><strong>Delete</strong> - Used to delete an entry from the directory. In order to do this, the LDAP client has to transmit a perfectly composed delete request to the server.</li>
<li><strong>Modify</strong> - Used by LDAP clients to make a request for making changes to the already existing database. The change to be made must be one of the following operations: add (including a new value), delete (deleting an already existing value), replace ( overwriting an existing value with a new one)</li>
<li><strong>Bind</strong> - on connection with the LDAP server, the default authentication state of the session is anonymous. There are basically two types of LDAP authentication methods - the simple authentication method and the SASL authentication method.</li>
<li><strong>Unbind</strong> -  this is the inverse of the bind operation. Unbind aborts any existing operations and terminates the connection, leaving no response in the end.</li>
</ul>
<p><strong>Bind</strong> is a relative important concept. lets simply understand it as a way of authentication, only Binded user has the permission to search some directory.</p>
<p><em>for example, "ou=people,dc=example, dc=com" this directory we defined as can be accessed as Anonymous , the use is to authenticate user, and "ou=group,dc=example, dc=com" will be defined as accessed by authenticated user. so when researching, we have to bind or user to "ou=people,dc=example, dc=com" at first to be able to do real search.</em></p>
<p><span style="color: #808080;"><em>** for how to configure these directory rules, you have to read later "<strong>OpenLdap using OLC (cn=config)</strong>"</em></span></p>
<h4><span style="line-height: 1.6em; color: #008000;">Using LDAPSearch</span></h4>
<pre><a href="http://www.openldap.org/software/man.cgi?query=ldapsearch&amp;apropos=0&amp;sektion=0&amp;manpath=OpenLDAP+2.0-Release&amp;format=html#end" name="NAME"><b>NAME</b></a>
       ldapsearch - LDAP search tool

<a href="http://www.openldap.org/software/man.cgi?query=ldapsearch&amp;apropos=0&amp;sektion=0&amp;manpath=OpenLDAP+2.0-Release&amp;format=html#end" name="SYNOPSIS"><b>SYNOPSIS</b></a>
       <b>ldapsearch</b>  [<b>-n</b>]  [<b>-u</b>] [<b>-v</b>] [<b>-k</b>] [<b>-K</b>] [<b>-t</b>] [<b>-A</b>] [<b>-C</b>] [<b>-L[L[L]]</b>] [<b>-M[M]</b>]
       [<b>-d</b> <i>debuglevel</i>] [<b>-f</b> <i>file</i>] [<b>-D</b> <i>binddn</i>] [<b>-W</b>] [<b>-w</b> <i>bindpasswd</i>] [<b>-H</b> <i>ldapuri</i>]
       [<b>-h</b> <i>ldaphost</i>]  [<b>-p</b> <i>ldapport</i>] [<b>-P</b> <i>2</i>|<i>3</i>] [<b>-b</b> <i>searchbase</i>] [<b>-s</b> <i>base</i>|<i>one</i>|<i>sub</i>]
       [<b>-a</b> <i>never</i>|<i>always</i>|<i>search</i>|<i>find</i>] [<b>-l</b> <i>timelimit</i>]  [<b>-z</b> <i>sizelimit</i>]  [<b>-O</b> secu-
       rity-properties<b>]</b>  [<b>-I</b>]  [<b>-Q</b>]  [<b>-U</b> <i>username</i>] [<b>-x</b>] [<b>-X</b> <i>authzid</i>] [<b>-Y</b> <i>mech</i>]
       [<b>-Z[Z]</b>] <i>filter</i> [<i>attrs...</i>]
<a href="http://www.openldap.org/software/man.cgi?query=ldapsearch&amp;apropos=0&amp;sektion=0&amp;manpath=OpenLDAP+2.0-Release&amp;format=html#end" name="DESCRIPTION"><b>
</b></a></pre>
<p>The parameter we have to aware is <strong>-b</strong>, <strong>-D</strong> and <strong>-x</strong>. if we don't use -x, then ldapsearch will use SASL.</p>
<p>Let's see some exaples :</p>
<p><strong>Search with Bind :</strong></p>
<pre class="brush:shell">ldapsearch -H ldaps://xxx.xxx.dev:636 -b "ou=whitepages,dc=example,dc=com" -D "uid=123456,ou=people,dc=example,dc=com" -w JW3p497s -x "uid=*"</pre>
<p><strong>Using filter:</strong></p>
<pre class="brush:shell">ldapsearch -LLL -s one -b "c=US" "(o=University*)" o description

ldapsearch -x -h 10.2.250.100 -b o=spm -LLL "(&amp;(objectclass=inetorgperson)(mail=*))" mail | grep 'mail:'</pre>
<p>There's really too many to talk about search, I dont want to write down here, just remember to use shell manual. want to know more, please read more at <a title="using ldapsearch" href="http://www.centos.org/docs/5/html/CDS/ag/8.0/Finding_Directory_Entries-Using_ldapsearch.html#Using_ldapsearch-Using_Special_Characters" target="_blank">using ldapsearch</a></p>
<h4><span style="color: #008000;">OpenLDAP using OLC (cn=config)</span></h4>
<p>When checking OpenLDAP configuration, I was confused about it. Later I found it using OLC. OLC is introduced after openladp 2.3, means online configuration. So we can do real deployment without restart.</p>
<p>in OLC configuration, it will define schema, data store location, and permission.  Just try to find out under your /etc/openldap directory.</p>
<p>read more about OLC at <a title="ldap olc" href="http://www.zytrax.com/books/ldap/ch6/slapd-config.html#intro" target="_blank">here</a></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>At last, there's really more about how LDAP works and LDAP configuration questions I haven't find out. Here, just give a basic understanding, and you need practise more ldapsearch by yourself.</p>
<p>But that's enough at this moment and let's do it later.</p>
<p>&nbsp;</p>
