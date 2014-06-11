---
layout: post
title: A few Bash skills should be remembered
categories:
- LINUX
tags:
- Linux
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
<h3><span style="color: #008000;">1. sudo !!</span></h3>
<div id="_mcePaste">How to recall the previous command? This is the one the most cool way.</div>
<div id="_mcePaste">The "!!" is a special feature which called event designators. And it equals  "!-1" , so it means you can also use "!-2","!-50","!-250" ... Usually, system will store 500 latest used commands in ~/bash_history.</div>
<h3><span style="color: #008000;">2. cd -</span></h3>
<div id="_mcePaste">This is the way to go back the directory where you just been.</div>
<h3><span style="color: #008000;">3. time read</span></h3>
<div id="_mcePaste">A easy timer. Caculate time until press enter.</div>
<h3><span style="color: #008000;">4. history | awk '{a[$2]++}END{for(i in a){print a[i] " " i}}' | sort -rn | head</span></h3>
<div id="_mcePaste">Show the top 10 most used commands.</div>
<h3><span style="color: #008000;">5. sudo netstat -tulnp</span></h3>
<div id="_mcePaste">Show the threads occupying ports.</div>
<div id="_mcePaste">-t: show TCP connection information</div>
<div id="_mcePaste">-u: show UDP connection information</div>
<div id="_mcePaste">-l: show monitoring ports</div>
<div id="_mcePaste">-n: show ip directly</div>
<div id="_mcePaste">-p: show thread PID and name ,need root user</div>
<h3><span style="color: #008000;">6. top</span></h3>
<div id="_mcePaste">Show the most used memory programs.</div>
<div id="_mcePaste">or you can do this : <strong>ps aux | sort -nk +4 | tail</strong></div>
<div><strong><br />
</strong></div>
<h3><span style="color: #008000;">7. The hot key should also remember:</span></h3>
<div id="_mcePaste">Ctrl + A Go to the beginning of the line you are currently typing on</div>
<div id="_mcePaste">Ctrl + E Go to the end of the line you are currently typing on</div>
<div id="_mcePaste">Ctrl + L    Clears the Screen, similar to the clear command</div>
<div id="_mcePaste">Ctrl + U Clears the line before the cursor position.</div>
<div id="_mcePaste">Ctrl + H Same as backspace</div>
<div id="_mcePaste">Ctrl + R Let’s you search through previously used commands</div>
<div id="_mcePaste">Ctrl + C Kill whatever you are running</div>
<div id="_mcePaste">Ctrl + D Exit the current shell</div>
<div id="_mcePaste">Ctrl + Z Puts whatever you are running into a suspended background process. fg restores it.</div>
<div id="_mcePaste">Ctrl + W Delete the word before the cursor</div>
<div id="_mcePaste">Ctrl + K Clear the line after the cursor</div>
<div id="_mcePaste">Ctrl + T Swap the last two characters before the cursor</div>
<div id="_mcePaste">Ctrl + P    Show previous command</div>
<div id="_mcePaste">Ctrl + N   Show next command</div>
<div id="_mcePaste">Tab Auto-complete files and folder names</div>
