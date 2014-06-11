---
layout: post
title: Migrate Zimbra from 32bit to 64bit
categories:
- OTHER
tags:
- Bash
- Zimbra
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
<p>Trying to migrate 32bit Zimbra Mailbox to 64bit Zimbra. You can migrate LDAP data first which including all the accounts and then migrate Mailbox which including messages, calendars ... etc</p>
<p>I assume you using the same version of Zimbra with both 32 bit and 64  bit. But it should be able to work for all version &gt; 6.0</p>
<h3><span style="color: #ff0000;"><strong>Migrate LDAP Data</strong></span></h3>
<p>&nbsp;</p>
<h4><strong><span style="color: #993300;">On 32 bit Zimbra : </span></strong></h4>
<h5><span style="color: #808000;"><strong>Export LDAP data in 32bit Zimbra</strong></span></h5>
<pre class="brush:shell">su - zimbra
/opt/zimbra/libexec/zmslapcat /tmp/
chown username:username /tmp/ldap.bak</pre>
<h4 class="brush:shell"><span style="color: #993300;"><strong>On 64 bit Zimbra:</strong></span></h4>
<h5><span style="color: #808000;"><strong>Copy the LDAP data to 64bit Zimbra</strong></span></h5>
<pre class="brush:shell">scp -P 32 &lt;username&gt;@&lt;64bit zimbra&gt;:/tmp/ldap.bak /tmp/ldap.bak</pre>
<h5><span style="color: #808000;"><strong>Replace the old hostname with the new one</strong></span></h5>
<pre class="brush:shell">sed -i 's/&lt;32bit zimbra name&gt;/&lt;64bit zimbra name&gt;/g' /tmp/ldap.bak</pre>
<h5><span style="color: #808000;"><strong>Backup LDAP passwords</strong></span></h5>
<pre class="brush:shell">su - zimbra
zmlocalconfig -s | grep password &gt; /opt/zimbra/backup/zmlocalconfig-pass.txt
zmcontrol stop</pre>
<h5><span style="color: #808000;"><strong>Backup LDAP database and then empty it</strong></span></h5>
<pre class="brush:shell">mv /opt/zimbra/data/ldap/hdb/ /opt/zimbra/data/ldap/hdb.backup/
mkdir -p /opt/zimbra/data/ldap/hdb/db/
mkdir -p /opt/zimbra/data/ldap/hdb/logs/
cp /opt/zimbra/data/ldap/hdb.backup/db/DB_CONFIG /opt/zimbra/data/ldap/hdb/db/.
exit</pre>
<h5><span style="color: #808000;"><strong>Import the LDAP database from the old environment</strong></span></h5>
<pre class="brush:shell">/opt/zimbra/openldap/sbin/slapadd -q -b '' -F /opt/zimbra/data/ldap/config -cv -l /tmp/ldap.bak &gt; /var/log/zimbra-ldap-import.log
chown -R zimbra:zimbra /opt/zimbra/data/ldap/hdb/db/</pre>
<h5><span style="color: #808000;"><strong>Restore LDAP passwords</strong></span></h5>
<pre class="brush:shell">su - zimbra
zmldappasswd $(grep zimbra_ldap_password /opt/zimbra/backup/zmlocalconfig-pass.txt | cut -d= -f 2)
zmldappasswd -r $(grep ldap_root_password /opt/zimbra/backup/zmlocalconfig-pass.txt | cut -d= -f 2)
zmldappasswd -p $(grep ldap_postfix_password /opt/zimbra/backup/zmlocalconfig-pass.txt | cut -d= -f 2)
zmldappasswd -a $(grep ldap_amavis_password /opt/zimbra/backup/zmlocalconfig-pass.txt | cut -d= -f 2)
zmldappasswd -l $(grep ldap_replication_password /opt/zimbra/backup/zmlocalconfig-pass.txt | cut -d= -f 2)
zmldappasswd -n $(grep ldap_nginx_password /opt/zimbra/backup/zmlocalconfig-pass.txt | cut -d= -f 2)
zmcontrol start</pre>
<p>&nbsp;</p>
<h3><span class="Apple-style-span" style="font-size: 21px; line-height: 25px; color: #ff0000;"><strong>Migrate Mailbox Data</strong></span></h3>
<p>Here we write bash script to use the zimbra export and import tool.</p>
<h4><span style="color: #993300;"><strong>On 32 bit Zimbra : </strong></span></h4>
<h5><span style="color: #808000;"><strong>Mailbox Export Script</strong></span></h5>
<pre class="brush:shell">#!/bin/bash
### START CONFIGURATION ###
DIR="/zimbra-mailbox-backup";
### END OF CONFIGURATION ###

USERS=`su - zimbra -c 'zmprov -l gaa'`;
DATE=`date +%Y%m%d`;

if [ ! -d $DIR ]; then mkdir $DIR; chown zimbra:zimbra $DIR; fi

for ACCOUNT in $USERS; do
NAME=`echo $ACCOUNT`;
echo "Processing mailbox $NAME backup..."
su - zimbra -c "zmmailbox -z -m $ACCOUNT getRestURL '//?fmt=tgz' &gt; $DIR/$NAME.tgz";
done

echo "Zimbra mailbox backup has been completed successfully."</pre>
<pre></pre>
<h4><span style="color: #993300;"><strong>On 64 bit Zimbra : </strong></span></h4>
<h5><span style="color: #808000;"><strong>Mailbox Import Script</strong></span></h5>
<pre class="brush:shell">#!/bin/bash
### START CONFIGURATION, CHANGE THE FOLDER WITH YOUR BACKUP FOLDER ###
DIR="/tmp/zimbra-mailbox-backup";
### END OF CONFIGURATION ###

clear

echo "Retrieve zimbra user name..."

USERS=`su - zimbra -c 'zmprov -l gaa'`;

for ACCOUNT in $USERS; do
NAME=`echo $ACCOUNT`;
echo "Restoring $NAME mailbox..."
su - zimbra -c "zmmailbox -z -m $NAME postRestURL '//?fmt=tgz&amp;resolve=reset' $DIR/$NAME.tgz";
done
echo "All mailbox has been restored successfully"</pre>
