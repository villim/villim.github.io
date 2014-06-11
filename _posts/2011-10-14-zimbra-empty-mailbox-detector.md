---
layout: post
title: Zimbra Empty Mailbox Detector
categories:
- PYTHON
tags:
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
<p>In last blog we already talking about <a title="Migrate Zimbra from 32bit to 64bit" href="http://www.from0to1.net/migrate-zimbra-from-32bit-to-64bit/" target="_blank">Migrate Zimbra from 32bit to 64bit</a> , however <strong>Zmmailbox</strong> is quite slow when export and import when you have greate many mailboxes. Each mailbox will cost 5 second, so when you have for example more than 10000 account, that would be a disaster. In Zimbra official documentation, it also mentioned, when migrate 30GB data, will cost 5 days and night.</p>
<p>There would be a few ways to accelerate the speed, but it always be a good idea to find out how many data you are facing. The empty mailbox you wont need to migrate mailbox. That's why we can create a script to find out the list of non-empty mailbox account.</p>
<p>Still, I'm using Python to do it.</p>
<pre class="brush:py">import os

# Get all accounts in zimbra and write into file
accounts=os.popen('su - zimbra -c "zmprov -l gaa"').read()
file = open('/root/zimbra.all.accounts.txt', 'w')
file.write(accounts)
file.close()

# Iterate to find account with mailbox
wholeAccounts= open('/root/zimbra.all.accounts.txt')
accountsWithMailBox = open('/root/zimbra.accounts.with.mailbox.txt','a')

for line in wholeAccounts:
        try:
                cmd = 'su - zimbra -c "zmmailbox -z -m %s gms"' % line.strip('\n')
                sizeofmailbox = os.popen(cmd).read().strip('\n')

                if sizeofmailbox &lt;&gt; '0 B':
                        print '%s is not empty and the size is %s ' % (line.strip('\n'), sizeofmailbox)
                        accountsWithMailBox.write(line)
                else:
                        print 'skip %s ' % line.strip('\n')
        except:
                print 'encounter exception with %s ' % line.strip('\n')

wholeAccounts.close()
accountsWithMailBox.close()</pre>
