---
layout: post
title: Vim with Multi-Language
categories:
- AGILE
- BOOK
- NOTES
- OTHER
- PHONE
tags: []
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
<p>因为最近同时在看几个语言，不能不考虑一下IDE的问题，实在不想装上一大堆莫名其妙的东西，浪费空间又得不停夏吓折腾。于是考虑还是 Vim，不拿它来写代码，感觉也没机会烂熟于心，Good Chance ~</p>
<p>&nbsp;</p>
<h5><span style="color: #993300;"><strong>不过首先有两个问题要解决：</strong></span></h5>
<ol>
<li><em>如果区分多种语言？ 每个语言有不同的配置，插件业各不相同，假如 Python 和 Php 的调试插件不相同，那么快捷键之类的设置一定会冲突。必须要能根据不同语言来定制，理想状态要把快捷键尽可能和 Eclipse 快捷键统一起来。免得搞得太混乱。</em></li>
<li><em>如何在不同设备里同步Vim配置？ 我可能用到 Vim 的设备还是挺多的：Mac Pro、公司台机、公司国外的远程链接、家里的台机，最近还在玩 iPhone 的版本，平板的版本。如果每一个都要重新配置一下，那肯定是要死人的。何况对于不同语言应该用什么样的插件我都还不明朗，要慢慢才能丰富起来。</em></li>
</ol>
<h5></h5>
<h5><span style="color: #008000;"><strong>问题1：区分多种语言 </strong></span></h5>
<p>就我所知解决方法有两种，可以直接在 .vimrc 里添加</p>
<pre class="brush:shell">autocmd FileType * set tabstop=2|set shiftwidth=2|set noexpandtab
autocmd FileType python set tabstop=4|set shiftwidth=4|set expandtab
au BufEnter *.py set ai sw=4 ts=4 sta et fo=croql</pre>
<p>毫无疑问，vimrc 会变成一个可怕的大文件，所以用ftplugin 方式更好一些，只需要根据语言的名字定义一个配置文件即可, 比如这个 python.vim：</p>
<pre class="brush:plain">" File ~/.vim/ftplugin/python.vim
" ($HOME/vimfiles/ftplugin/python.vim on Windows)
" Python specific settings

setlocal tabstop=2
setlocal shiftwidth=2
setlocal expandtab
setlocal autoindent
setlocal smarttab
setlocal formatoptions=croql

let g:pymode_folding = 0</pre>
<p>如果是 Vim 不能识别的语言，那么配置一个自己的语言，请参考文档。</p>
<p>如果你熟悉 Vim Python 的大部分配置，只想复写某些配置那么将 python.vim 放到：</p>
<pre class="brush:shell">.vim/after/ftplugin/python.vim</pre>
<p><span style="color: #ff0000;">注意</span>，以上配置需要在 .vimrc 中添加一下配置：</p>
<pre class="brush:shell">filetype plugin indent on</pre>
<p>将python相关的配置放这里可以解决，同一个插件不同的快捷键，或者同一快捷键对应不同的插件。</p>
<p>P.S. 文中 Vim 配置都以 Mac 和 Linux 为例，Windows 路径为 $HOME/vimfiles</p>
<h5></h5>
<h5><span style="color: #008000;"><strong>问题2： 同步Vim配置</strong></span></h5>
<p>毫无疑问，用 GitHub 啦！首先，使用 <a title="vim-pathogen" href="https://github.com/tpope/vim-pathogen" target="_blank">Pathogen</a> 来管理插件，真的简单好用，请参考项目安装文档。</p>
<p>Pathogen 的文档建议按照以下方式安装插件，比如：</p>
<pre class="brush:shell">cd ~/.vim/bundle
git clone git:/github.com/tpope/vim-fugitive.git</pre>
<p><strong>我们改用 submodule 的方式添加</strong>：</p>
<pre class="brush:shell">cd ~/.vim
git submodule init
git submodule add git://github.com/tpope/vim-fugitive.git bundle/vim-fugitive
git commit -m 'Added vim-fugitive
git push</pre>
<p><strong>在其他机器上同步时只需要</strong>：</p>
<pre class="brush:shell">git clone git@github.com:villim/dotvim.git ~/.vim
cd ~/.vim
git submodule init
git submodule update</pre>
<p>&nbsp;</p>
<p><strong><span style="color: #993300;">我的Github配置项目：</span></strong><br />
My dotvim project link at <a title="dotvim" href="https://github.com/villim/dotvim" target="_blank">HERE</a></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
