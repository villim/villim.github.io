---
layout: post
title: VIM Configuration for C
categories:
- C/C++
- LINUX
tags:
- C
- Vim
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
<p>Update /etc/vim/vimrc with following configuration:</p>
<pre class="brush:plain"> 40 " The following are commented out as they cause vim to behave a lot
 41 " differently from regular Vi. They are highly recommended though.
 42 "set showcmd        " Show (partial) command in status line.
 43 set showmatch       " Show matching brackets.
 44 "set ignorecase     " Do case insensitive matching
 45 "set smartcase      " Do smart case matching
 46 "set incsearch      " Incremental search
 47 "set autowrite      " Automatically save before commands like :next and :make
 48 "set hidden             " Hide buffers when they are abandoned
 49 "set mouse=a        " Enable mouse usage (all modes)
 50 set number      " Show row number
 51 set tabstop=4       " Set Tab as 4
 52 set softtabstop=4   " Set Soft Tab as 4
 53 set autoindent      " Set auto indent
 54 set cindent     " Using auto indent as C and C++ language
 55 set cinoptions={0,1s,t0,n-2,p2s,(03s,=.5s,&gt;1s,=1s,:1s   " Set defined indent as C and C++ language</pre>
