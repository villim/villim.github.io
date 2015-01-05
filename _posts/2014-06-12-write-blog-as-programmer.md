---
layout: post
titile: Writter Blog as Programmer
---

### Be cool with Writting

**Wrriting is cool, but it's much cooler to do cool wrriting.**

#### WordPress
Infact WordPress is not that bad, if you only concerns about the content. You can easy manage your website, and there's quite a lot hoster any where you can buy, it has plenty of free skins and 3rd party tools. It's already very very mature, also easy and some kind of cool to create your own blog service.

And it's not too expensive. I pay 100RMB for a 600M spaces, and 60RMB for my domain name "from0to1.net" per year.  

Ok, and here comes to **BUT** ^_^ 

But if you concerns details, it's not that beauty under the surface. 

* The most urgly stuff is the generated THML codes by WordPress. After modify and remodify your posts for serveral times, there will be great many duplicated tags. Makes you almost impossible to reuse it. 
* Though it's cheap, but still cost money
* emmm, it's not cool any more ~.~ 

#### Static Pages + Markdown
If your blogger isn't something matter and just a place to note down your thoughts, then you don't need dynamic website as WordPress. Static pages hosted by free Github already good enough.

* **It's free** 
* Using Mardown to write, original file is much much more friendly
* Data stored in Github, don't worry about backup anymore
* **no flow limited**
* **The most, It's cool to blog like programming!!!**

Don't waste time anymore, let's do it~

### Jekyll + Github

<p style="color:red"><Strong>Becareful: following instruction only tested with Mac</strong></p>

#### Install Jekyll

##### Install Ruby
Ruby is required, Mac already installed Ruby, if you don't have it, need <a title="Install Ruby" herf="http://www.rubyinstaller.org/downloads/" target="_blank">install by yourself</a>

##### Install Jekyll
{% highlight bash %}
	
	sudo gem install jekyll
	sudo gem install bundler // Not necessary, but I will use later
	sudo gem install github-pages
	jekyll new test-site
	cd test-site
	jekyll serve
	# Browse to http://localhost:4000 you should see it's working now
		
{% endhighlight %}

#### Creating Github Pages

Install Git and Using Github is easy, just read <a tile="Github documents" href="https://github.com/" targe="_blank"> Github's documents </a> carefully, and following step by step.

Find how Gibthub Pages work costing me a lot of time. But infact, it's not deficult, there're two kinds of Pages you can use.

##### Project Pages
Every project can create it's own page, but the branch must be **gh-pages**
{% highlight bash %}
	
	$ git init
	$ git checkout --orphan gh-pages
	$ git remote add origin https://github.com/username/jekyll_demo.git
	$ git push origin gh-pages
	
{% endhighlight %}

Github we generate url with project name like this :
	
	https://user.github.io/projectname/
it means you need configure your Jekyll **_config.yml** with

	baseurl=/projectname
and then when you create your Jekyll template you need use `'site.baseurl'` instead of `'\'`

#### User Pages
User Pages must create repository as name : **UserName.github.io**

Each user can create only one User Page. And you don't need set baseurl anymore.

{% highlight bash %}
	
	$ git init	
	$ git checkout master
	$ git remote add origin https://github.com/username/username.github.io
	$ git push origin master
	
{% endhighlight %}

#### Create your Website

The easiest way is clone somebody's Git repository and see how it works.

Or you can refer to Jekyll's documentation, or the end of this artical and following Ruanyifeng's instrument to build the simplest one.

I suggest you build it by yourself from the beginning, and you will earn much more than you expected.

#### Migarte from Wordpress

At first, I want to use <a title="WordPress to Jekyll Exporter" href="https://github.com/benbalter/wordpress-to-jekyll-exporter" target="_">WordPress to Jekyll Exporter </a>. However, I encounter ERROR when activating the plugin, seems caused by PHP version problem.

Then I tried <a title="Jekyll Importer Tool" href="http://import.jekyllrb.com/" target="_blank">Jekyll Importer tool</a>

1. Got to your WordPress Admin Dashboard
2. Tools -> Export -> Choose 'All content' -> Download Export File (mine is from0to1.wordpress.2014-06-11.xml)
3. Run following script

{% highlight bash %}
		
	$ cd tempdir
	$ ruby -rubygems -e 'require "jekyll-import"; 	JekyllImport::Importers::WordpressDotCom.run({ "source" => "/Users/villim/	Documents/from0to1.wordpress.2014-06-11.xml" })'
	
{% endhighlight %}

Then you will find all posts in **tempdir** 

However, the generated files are not perfect. You may still need modify manually.

#### Configure Domain Names
If you want to use your specify domain name, You can buy it on godaddy.com, learn more about godaddy at <a title="Godaddy Usage" href="http://www.siqiboke.com/post/20.html" target="_blank">here</a>.

And just configure as <a title="Setup a custom domain" href="https://help.github.com/articles/setting-up-a-custom-domain-with-github-pages" target="_blank" >Github's document </a>

### Developing Tips
##### css
For me, I really not familiar with CSS stuff. Although I also have to read them now and then. So I spend most of my time learning it and to setup page frame, to supporting code area, using beautify icons ... although currect site still quite simple.

And I do enjoy this progress. I learn a lot from this site : <a href="http://www.456bereastreet.com/lab/developing_with_web_standards/csslayout/2-col/" target="_blank">456 BEREA</a>

##### Pygments
In order to make code area beautiful, there're many ways, directly using JavaScript is also possible, but after tried, I stick to using official way, Pygments.
	{% highlight bash %}
		
	$ easy_install Pygments	
	$ python   //checking what styles can be used
	>>> from pygments.styles import STYLE_MAP
	>>> STYLE_MAP.keys()
	['monokai', 'manni', 'rrt', 'perldoc', 'borland', 'colorful', 'default', 'murphy', 'vs', 'trac', 'tango', 'fruity', 'autumn', 'bw', 'emacs', 'vim', 'pastie', 'friendly', 'native']
	
	// generate the highlighting css file to your project directory
	$ pygmentize -S friendly -f html > /project-dir/css/Pygments.css
	{% endhighlight %}
	
After that, just include it in **_layout/defalut.html**

	<link href="/css/pygmentize.css" media="screen, projection" rel="stylesheet" type="text/css" />

When you want some code to be highlighted, do as following:

	\{ % highlight python % \}   --'\{' means '{'
		//some code
	\{ % endhighlight % \}

	
##### Jekyll-post-links  	
In order to link to your own post easily, like:
	
	\{ % post_links filename description % \}	
try <a title="Jekyll-post-links" href="http://brm.io/jekyll-post-links/" target="_blank">Jekyll-post-links</a>

##### Debug efficiently
In order to checking your post easily and don't need to restart Jekyll every time.

First, create a Gemfile

	#Gemfile
	source 'https://rubygems.org'
	gem 'github-pages'

And then create serve.sh
	
	#serve.sh
	#!/bin/bash
	bundle exec jekyll serve -w --draft 

Then you just need to run the serve.sh and leave it alone, when posts changes, it will regenerate automatically

	$ sh serve.sh


##### Renaming files surfix

After importing the WordPress data, these posts are all endwith `.html`

So I create a script to renaming automactically:
{% highlight bash %}
	
	$ python
    >>> import os
    >>> for filename in os.listdir("/Users/villim/WORK/villim.github.io/_posts/"):
	...     (root, ext) = os.path.splitext(filename)
	...     os.rename(filename, root+'.md')
	... 
	
{% endhighlight %}

### Personal Feeling

Spend almost 5 days, finanlly finish migration to this usable site. It was a really nice feeling.

While I create new Blog like this one with markdown, and using Git everyday, it's really just like coding, wounderful!

About markdown, however, it don't have a sytax to create a link opened in another tab. So I still have to `<a href></a>` at this moment. Hoping will find a way to solve it.
 
And Ruby seems quite easy for WEB developing, later may have a look at it.

### Reference
<a href="http://jekyllrb.com/" target="_blank">**Jekyll Official Site:**</a>

has all the information you need to know. Know more about Liquid, if you need create your own templates

<a href="http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html" target="_blank">**Ruanyifeng Blogging with Jekyll:** </a>

This artical will give a brief intro enough to start as a blind.


