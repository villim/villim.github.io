---
layout: post
title: Registers in Vim
categories:
- LINUX
tags:
- Vim
status: publish
type: post
published: true
meta:
  _wp_old_slug: ''
author:
  login: villim
  email: villim@126.com
  display_name: Villim
  first_name: Villim
  last_name: Wong
---
<p>When using Vim and GVim, it's really disturbing that the copied text with Ctrl+C can't be pasted into Vim with "p" . What's the XXX hell happened?</p>
<p>This command is able to show the details in registers:</p>
<pre class="brush:shell">:reg</pre>
<p>you'll see following similar output , it list the information stored in all registers :</p>
<pre class="brush:shell">--- Registers ---
""   the default register
"0   ^J
"1   h^J^J^Jdebttptutneraraverick
"2   h^J^J^Jdebttptutnerar
"3   h^J^J^Jdebttptutner
"4   h^J^J^Jdebttptu
"5   h^J^J^Jdebttp
"6   ^J^J^Jdeb
"7   n^Jdebttptutneraraverick
"8   using the eighth register
"9   n^Jdebttptutnerar
"-   m
"*   INFO] Total time: 38 seconds
"+   INFO] Total time: 38 seconds
":   reg
"%   test.test
"/   centralAuthenticationService</pre>
<p>When we just yank with ' <em><strong>y</strong></em> ' in Vim, it will be copied to the "" register, so when put with '<em><strong>p</strong></em>', will print "the default register"</p>
<p>But you can also yank with '  <strong><em>y"8</em></strong> ' , and put with '  <strong><em>"8p</em></strong> '. Then it'll print "using the eighth register"</p>
<p>When we using <strong><em>Ctrl+C</em></strong> , the text will be copied to the system register '  <strong><em>"+ </em></strong>' , so we have to put with ' <strong><em> "+p</em></strong> '<br />
If you are in <strong><em>edit mode</em></strong> , you can use <strong><em>Shfit+Insert</em></strong> to copy the content in system register.</p>
