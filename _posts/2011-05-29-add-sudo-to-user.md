---
layout: post
title: Add SUDO to User
categories:
- LINUX
tags:
- SUDO
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
<p>Ubuntu don't allow you to operation system directly using "root" user in the safe's sake.</p>
<p>Thus, you need use "SUDO" command, to act like operating with root rights. And don't have to change to root user. This is definitely a brilliant idea. You can check the sudo list by using command :</p>
<pre class="brush:shell">less  /etc/sudoers</pre>
<p>The file looks like following :</p>
<pre class="brush:plain"># /etc/sudoers
#
# This file MUST be edited with the 'visudo' command as root.
#
# See the man page for details on how to write a sudoers file.
#

Defaults        env_reset

# Host alias specification

# User alias specification

# Cmnd alias specification

# User privilege specification
root    ALL=(ALL) ALL

# Allow members of group sudo to execute any command
# (Note that later entries override this, so you might need to move
# it further down)
%sudo ALL=(ALL) ALL
#
#includedir /etc/sudoers.d

# Members of the admin group may gain root privileges
%admin ALL=(ALL) ALL</pre>
<p>As the comment you can see,  must use visudo command as root user to modify this file :</p>
<pre class="brush:shell">sudo visudo</pre>
<p>We can see following line, what does it mean?</p>
<pre class="brush:shell"># User privilege specification
root    ALL=(ALL) ALL</pre>
<p>It means user root can execute from ALL terminals, acting as ALL (any) users, and run ALL (any) command.</p>
<p>So the format is :</p>
<pre class="brush:plain">[user]  [terminal that use sudo]= ( [as which user he may act] ) [commands he may run]</pre>
<p>Some examples :</p>
<pre class="brush:shell">rhoneldo ALL=(OP) ALL
# The user rhoneldo can run any command from any terminal as any user in the OP group (root or operator).

zidane OFNET=(ALL) ALL
# user zidane may run any command from any machine in the
OFNET network, as any user.

backham ALL= PRINTING
# user backham may run lpc and lprm from any machine.

nakata ALL=(ALL) ALL NO PASSWD: ALL
# do not ask to fill password when user nakata using sudo</pre>
