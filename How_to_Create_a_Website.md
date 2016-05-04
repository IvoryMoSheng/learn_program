#How to Create a Website
---
1. Domain 域名
2. Web Host 网络主机/虚拟主机
3. Website Software and Your Own Email 网站软件和电子邮件
	- 博客程序 wordpress
4. Website Design and Contents 网页设计和内容

---
##github和Jekyll入门
###github
github是一个具有版本管理功能的代码仓库，每个项目都有一个主页，列出项目的源文件。  
github Pages被认为是用户编写的、托管在github上的静态网页。允许用户自定义项目首页，用来替代默认的源码列表。一个简明易懂的网页，说明每一步应该怎么做。  
github提供模板，允许站内生成网页，但也允许用户自己编写网页，然后上传。这种上传并不是单纯的上传，而是会经过Jekyll程序的再处理。
###Jekyll
Jekyll是一个静态站点生成器，它会根据网页源码生成静态文件。它提供了模板、变量、插件等功能，所以实际上可以用来编写整个网站。
###思路
先在本地编写符合Jekyll规范的网站源码，然后上传到github，由github生成并托管整个网站。
###优点
- 免费，无限流量。
- 享受git的版本管理功能
- 用自己喜欢的编辑器写文章
###缺点
- 有一定技术门槛，你必须要懂一点git和网页开发。
- 它生成的是静态网页，添加动态功能必须使用外部服务，比如评论功能就只能用disqus。
- 它不适合大型网站，因为没有用到数据库，每运行一次都必须遍历全部的文本文件，网站越大，生成时间越长。

---
####一.创建项目
建立一个目录，作为项目的主目录

	$mkdir Jekyll
在该目录下，对目录进行Git初始化

	$cd Jekyll
	$git init
创建一个没有父节点的分支gh-pages。因为github规定，只有该分支中的页面，才会生成网页文件。后面的动作，都在该分支下完成。

	$git checkout --orphan gh-pages
####二.创建设置文件
在项目根目录下，建立一个名为_config.yml的文本文件。它是jekyll的设置文件，在里面填入如下内容，其他设置都可以用默认选项

	baseurl: /jekyll

目录结构

	/jekyll
		|-- _config.yml
###三.创建模板文件
在项目根目录下，创建一个_layouts目录，用于存放模板文件。

	$ mkdit _layouts
进入该目录，创建一个default.html文件，作为Blog的默认模板。

	　<!DOCTYPE html>
	　　<html>
	　　<head>
	　　　　<meta http-equiv="content-type" content="text/html; charset=utf-8" />
	　　　　<title>{{ page.title }}</title>
	　　</head>
	　　<body>
	
	　　　　{{ content }}
	
	　　</body>
	　　</html>
Jekyll使用Liquid模板语言，{{ page.title }}表示文章标题，{{ content }}表示文章内容。

目录结构

	　/jekyll_demo
	　　　　|--　_config.yml
	　　　　|--　_layouts
	　　　　|　　　|--　default.html
###四.创建文章。
回到项目根目录，创建一个_posts目录，用于存放blog文章。

	$ mkdir _posts
进入该目录，创建第一篇文章。文章就是普通的文本文件，文件名假定为2012-08-25-hello-world.html。(注意，文件名必须为"年-月-日-文章标题.后缀名"的格式。如果网页代码采用html格式，后缀名为html；如果采用markdown格式，后缀名为md。）

       ---
	　　layout: default
	　　title: 你好，世界
	　　---
	　　<h2>{{ page.title }}</h2>
	　　<p>我的第一篇文章</p>
	　　<p>{{ page.date | date_to_string }}</p>
每篇文章的头部，必须有一个yaml文件头，用来设置一些元数据。它用三根短划线"---"，标记开始和结束，里面每一行设置一种元数据。"layout:default"，表示该文章的模板使用_layouts目录下的default.html文件；"title: 你好，世界"，表示该文章的标题是"你好，世界"，如果不设置这个值，默认使用嵌入文件名的标题，即"hello world"。

在yaml文件头后面，就是文章的正式内容，里面可以使用模板变量。{{ page.title }}就是文件头中设置的"你好，世界"，{{ page.date }}则是嵌入文件名的日期（也可以在文件头重新定义date变量），"| date_to_string"表示将page.date变量转化成人类可读的格式。

目录结构

	/jekyll_demo
	　　　　|--　_config.yml
	　　　　|--　_layouts
	　　　　|　　　|--　default.html 
	　　　　|--　_posts
	　　　　|　　　|--　2012-08-25-hello-world.html
####五.创建主页
回到根目录，创建一个index.html文件

	---
	layout: default
	title: 我的Blog
	---
	<h2>{{ page.title }}</h2>
	<p>最新文章</p>
	<ul>
	　　{% for post in site.posts %}
	　　　　<li>{{ post.date | date_to_string }} <a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></li>
	　　　　{% endfor %}
	</ul>
Yaml文件头表示，首页使用default模板，标题为"我的Blog"。然后，首页使用了{% for post in site.posts %}，表示对所有帖子进行一个遍历。这里要注意的是，Liquid模板语言规定，输出内容使用两层大括号，单纯的命令使用一层大括号。至于{{site.baseurl}}就是_config.yml中设置的baseurl变量。

目录结构

	 /jekyll_demo
	　　　　|--　_config.yml
	　　　　|--　_layouts
	　　　　|　　　|--　default.html 
	　　　　|--　_posts
	　　　　|　　　|--　2012-08-25-hello-world.html
	　　　　|--　index.html
####六.发布内容
所有内容加入本地git库

	　$ git add .
	　$ git commit -m "first post"
前往github的网站，在网站上创建一个名为jekyll_demo的库。接着，再将本地内容推送到github上你刚创建的库。注意，下面命令中的username，要替换成你的username。

	$ git remote add origin https://github.com/username/jekyll_demo.git
	$ git push origin gh-pages
上传成功之后，等10分钟左右，访问http://username.github.com/jekyll_demo/就可以看到Blog已经生成了（将username换成你的用户名）。
####七，绑定域名
如果你不想用http://username.github.com/jekyll_demo/这个域名，可以换成自己的域名。  
具体方法是在repo的根目录下面，新建一个名为CNAME的文本文件，里面写入你要绑定的域名，比如example.com或者xxx.example.com。
如果绑定的是顶级域名，则DNS要新建一条A记录，指向204.232.175.78。如果绑定的是二级域名，则DNS要新建一条CNAME记录，指向username.github.com（请将username换成你的用户名）。此外，别忘了将_config.yml文件中的baseurl改成根目录"/"。
至此，最简单的Blog就算搭建完成了。进一步的完善，请参考Jekyll创始人的示例库，以及其他用Jekyll搭建的blog。
##