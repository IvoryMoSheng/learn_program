---
title: 使用Hexo和Github搭建独立博客之配置优化
date: 2016-05-03 13:27:16
tags:
categories: Hexo
toc: true
---
## 站点的配置
整站的配置hexo/_config.yml  
	
	
		# Hexo Configuration
	## Docs: https://hexo.io/docs/configuration.html
	## Source: https://github.com/hexojs/hexo/
	
	# Site 
	title: Ivory_MoSheng’s Blog #站点名
	subtitle: 优秀的人,不是不合群,而是他们合群的人里面没有你.
	description: make progress #站点描述，方便搜索引擎收录
	author: Ivory_MoSheng
	language: zh-CN
	timezone:
<!--more-->	
	# URL    绑定域名后，欲创建sitemap.xml需要配置该项
	## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
	url: http://ivorymosheng.com
	root: /
	permalink: :year/:month/:day/:title/
	permalink_defaults:
	
	# Directory
	source_dir: source
	public_dir: public
	tag_dir: tags
	archive_dir: archives
	category_dir: categories
	code_dir: downloads/code
	i18n_dir: :lang
	skip_render:
	
	# Writing  文章布局，写作格式的定义
	new_post_name: :title.md # File name of new posts
	default_layout: post
	titlecase: false # Transform title into titlecase
	external_link: true # Open external links in new tab
	filename_case: 0
	render_drafts: false
	post_asset_folder: false
	relative_link: false
	future: true
	highlight:
	  enable: true
	  line_number: true
	  auto_detect: false
	  tab_replace:
	
	# Category & Tag
	default_category: uncategorized
	category_map:
	tag_map:
	
	# Date / Time format 日期格式
	## Hexo uses Moment.js to parse and display date
	## You can customize the date format as defined in
	## http://momentjs.com/docs/#/displaying/format/
	date_format: YYYY-MM-DD
	time_format: HH:mm:ss
	
	# Pagination 每页显示的文章数
	## Set per_page to 0 to disable pagination
	per_page: 5
	pagination_dir: page
	
	# Extensions  配置插件和主题
	## Plugins: https://hexo.io/plugins/
	## Themes: https://hexo.io/themes/
	theme: landscape
	
	
	duoshuo_shortname: ivory2016
	# Deployment  部署到Github
	## Docs: https://hexo.io/docs/deployment.html
	deploy:
	  type: git
	  repo: git@github.com:IvoryMoSheng/IvoryMoSheng.github.io.git
	  branch: master

主题的配置hexo\themes\light_config.yml
	
			# Header
	menu:   站点顶部导航菜单
	  Home: /
	  Archives: /archives
	  about: /about
	rss: /atom.xml
	
	# Content
	excerpt_link: Read More
	fancybox: true
	
	# Sidebar  站点侧边导航栏
	sidebar: right
	widgets:
	- category
	- tag
	- tagcloud
	- archive
	- recent_posts
	- blogroll
	
	
	# display widgets at the bottom of index pages (pagination == 2)
	index_widgets:
	# - category
	# - tagcloud
	# - archive
	
	# widget behavior
	archive_type: 'monthly'
	show_count: false
	
	# Miscellaneous
	google_analytics:
	favicon: /favicon.png
	twitter:
	google_plus:
	fb_admins:
	fb_app_id:


## 添加多说评论系统
在Hexo\_config.yml中添加多说的配置：

	duoshuo_shortname: ivory2016  //你站点的short_name
修改themes\landscape\layout\_partial\article.ejs模板
把

	<% if (!index && post.comments && config.disqus_shortname){ %>
	  <section id="comments">
	    <div id="disqus_thread">
	      <noscript>Please enable JavaScript to view the <a href="//disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
	    </div>
	  </section>
	  <% } %>
修改为

	 <% if (!index && post.comments && config.duoshuo_shortname){ %>
	  <section id="comments">
	    <!-- 多说评论框 start -->
	    <div class="ds-thread" data-thread-key="<%= post.layout %>-<%= post.slug %>" data-title="<%= post.title %>" data-url="<%= page.permalink %>"></div>
	    <!-- 多说评论框 end -->
	    <!-- 多说公共JS代码 start (一个网页只需插入一次) -->
	    <script type="text/javascript">
	    var duoshuoQuery = {short_name:'<%= config.duoshuo_shortname %>'};
	      (function() {
	        var ds = document.createElement('script');
	        ds.type = 'text/javascript';ds.async = true;
	        ds.src = (document.location.protocol == 'https:' ? 'https:' : 'http:') + '//static.duoshuo.com/embed.js';
	        ds.charset = 'UTF-8';
	        (document.getElementsByTagName('head')[0] 
	         || document.getElementsByTagName('body')[0]).appendChild(ds);
	      })();
	      </script>
	    <!-- 多说公共JS代码 end -->
	  </section>
	  <% } %>

## 添加页面导航
在themes\landscape\layout\_partial\article.ejs模板中，添加

	<nav id="pagination" >
	    <% if (page.prev) { %>
	    <a href="<%- config.root %><%- page.prev.path %>" class="alignleft prev" ><%= __('prev') %></a>
	    <% } %>
	    <% if (page.next) { %>
	    <a href="<%- config.root %><%- page.next.path %>" class="alignright next" ><%= __('next') %></a>
	    <% } %>
	    <div class="clearfix"></div>
	</nav>
## 添加小图标
在Hexo\themes\landscape\layout\_partial\head.ejs里将<link rel="icon" href="<%- theme.favicon %>">替换为<link href="<%- config.root %>favicon.ico" rel="icon" type="image/x-ico">。将favicon.ico图标文件放在source目录下。制作图标的网站，http://www.faviconer.com。
## 添加“百度分享”（失败）
到百度分享获得代码，在exo\themes\landscape\layout\_partial\article.ejs中，将<%-partial('post/share')%>删掉，替换为百度分享的代码。
## 添加分类、标签云widget
在Hexo\themes\landscape\_config.yml中，添加

	widgets:
	- category
	- tagcloud
## 添加友情链接widget
在themes/landscape/layout/_widget中新建名为blogroll.ejs的文件，编辑内容如下：

	<div class="widget tag">
	<h3 class="title">友情链接</h3>
	<ul class="entry">
	<li><a href="http://www.baidu.com/" title="baidu">百度</a></li>
	</ul>
	</div>
在themes/landscape/_config.yml下，添加：

	widgets:
	- blogroll
## 生成post时默认生成categories配置项
在scaffolds/post.md中，添加一行categories:。同理可应用在page.md
## 添加新浪微博秀
去新浪微博开放平台设置和生成微博秀代码。
在themes/landscape/layout/_widget中新建名为weibo.ejs的文件，将刚才的代码直接保存到这里。
在themes/landscape/_config.yml中，添加如下：

	widgets:
	- weibo
## 导航栏添加”关于”
hexo new page "about"
到source/about/index.md编辑内容。
在themes/landscape/_config.yml中，添加如下：

	menu:
	  about: /about
## 主页文章显示摘要
编辑md文件的时候，在要作为摘要的文字后面添加
	
	<!--more-->
即可。
## 加入「fork me on github」(失败)
https://github.com/blog/273-github-ribbons有 github 给出的教程，把代码插入到任意一个全局的模板文件中就行，比如layout.ejs的末尾。
## 添加网站访客人数统计
获取代码http://www.amazingcounters.com/

添加代码到主题中  
为了方便的开启或者关闭访客数量统计功能我们可以在主题的配置文_config.yml里面添加一个变量，counter: true当改为false时即关闭了访客统计功能。

在\Hexo\themes\landscape\layout\_widget新建counter.ejs文件
配置主题下\Hexo\themes\landscape的_config.yml文件

	widgets:
	- counter

Your account settings have been saved. You do NOT have to change the code on your site. Just go to your web site and refresh your browser to see the changes.
## 速度优化(未使用)
Github page->Gitcafe Page


建议把 google 提供的 jquery 和 fonts api 全换掉
## 添加RSS(未使用)
hexo提供了RSS的生成插件，需要手动安装和设置。步骤如下：
安装RSS插件到本地：npm install hexo-generator-feed
开启RSS功能：编辑hexo/_config.yml，添加如下代码：

	plugins:
	- hexo-generator-feed
在站点添加链接：
在themes/light/_config.yml中，编辑 rss: /atom.xml
在themes/light/layout/_partial/header.ejs中，<ul></ul>之间，添加一样代码<li> <a href="/atom.xml">RSS</a> </li>
## 添加sitemap（未使用）
同样的，我们使用hexo提供的插件，方法与添加RSS类似。
安装sitemap到本地：npm install hexo-generator-sitemap
开启sitemap功能：编辑hexo/_config.yml，添加如下代码：

	plugins:
	- hexo-generator-sitemap
访问zipperary/sitemap.xml即可看到站点地图。不过，sitemap的初衷是给搜索引擎看的，为了提高搜索引擎对自己站点的收录效果，我们最好手动到google和百度等搜索引擎提交sitemap.xml。
## 设置百度统计、Google Analytics（未使用）
到百度统计和Google Analytics（可能需要穿墙）注册账号、添加网站地址即可，很简单，不详述了。需要注意的是，设置好之后数据要过几个小时才能出现，不用着急。
## 购买域名、设置DNS（未使用）
## 文章中插入图片（未使用）
使用markdown写文章，插入图片的格式为![图片名称](链接地址)，这里要说的是链接地址怎么写。对于hexo，有两种方式：

1. 使用本地路径：在hexo/source目录下新建一个img文件夹，将图片放入该文件夹下，插入图片时链接即为/img/图片名称。
2. 使用微博图床，地址http://weibotuchuang.sinaapp.com/，将图片拖入区域中，会生成图片的URL，这就是链接地址。
## 修改背景图片
在Hexo\themes\landscape\source\css\images添加所想设置的背景图片  
banner为顶部条幅图片
## Bug(未使用)
1. 「warning: LF will be replaced by CRLF」
在hexo deploy时，有时会出现这个提示信息warning: LF will be replaced by CRLF，虽然看起来挺乱糟糟的，但不影响使用，可以忽略不计。若想不提示，可以使用如下方法：
切换到博客的根目录，执行如下命令：git config --global core.autocrlf false
删除掉该目录下的.git文件夹（可能是隐藏的），命令：rm -rf .git
重新git init。
再deploy试试吧，清新脱俗了。
2. hexo deploy没反应
主要问题出在config.yml的deploy配置上。注意缩进，同时注意冒号后面要有一个空格。
3. hexo升级错误，Hexo命令失效
这种情况下，可执行npm install -g hexo重新安装一遍hexo，效果跟升级一样。各版本所做更新修正，
4. 搜索框进行搜索：没有结果
点击搜索后进入的google页面，搜索框里面是不是显示「site:yoursite.com」，这说明有个地方没有设置，请随我来：
打开根目录下的config文件，第15行，url:，自觉填上吧。
5. 代码块中不显示行号
使用四个空格的方式标志代码块的确没行号，需要行号的要使用反引号的方式。
## 更改标题样式
在Hexo\themes\landscape\source\css\_partial的article.styl 的 .article-entry 合适位置添加如下内容：

	h1
	  padding: 7px 6px 7px 0px;
	  background: #dddddd;
	h2
	  border-bottom: 1px #d8d8d8 solid;

实现在一级标题下加上浅色背景，二级标题下加浅色下划线，能使文章层次更加清晰，便于阅读。
## 为博客内容添加目录
Hexo博客系统的核心支持生成目录（Table of Contents），但其默认的主题Landscape并不支持目录的显示。我们只需对Landscape的主题文件稍作修改并添加一点目录的CSS就可以在文章前面显示友好的目录了。
### 修改Landscape主题的ejs文件
我们首先要编辑文章显示页面的模板，也就是themes/landscape/layout/_partial/article.ejs文件。为了将目录生成在正文之前，我们首先在这个文件中找到<%- post.content %>，并在这一行之前加入如下代码：

	<!-- Table of Contents -->
	<% if (!index && post.toc){ %>
	  <div id="toc" class="toc-article">
	    <strong class="toc-title">文章目录</strong>
	    <%- toc(post.content) %>
	  </div>
	<% } %>
这段代码的含义清晰明了，if语句中有两个条件，!index是为了不在首页的文章摘要中生成目录，post.toc确保了只在显式地标记了toc: true的文章中生成目录。若这两个条件满足，则创建一个目录的<div>。

修改完这个文件之后，找一篇包含了多个子标题的文章，并在文章开头的front-matter中添加一句toc: true，在浏览器中访问这篇文章，应该可以看到文章的开头处已经有了带链接的目录。但是这样的目录实在太难看，我们还需要添加相应的CSS来将其指定为我们想要的样式。
### 为目录编写CSS文件
要指定目录的样式，我们要修改的文件是themes/landscape/source/css/_partial/article.styl。在文件的最后，添加如下代码：

	/*toc*/
	.toc-article
	  background #eee
	  border 1px solid #bbb
	  border-radius 10px
	  margin 1.5em 0 0.3em 1.5em
	  padding 1.2em 1em 0 1em
	  max-width 28%
	
	.toc-title
	  font-size 120%
	
	#toc
	  line-height 1em
	  font-size 0.9em
	  float right
	  .toc
	    padding 0
	    margin 1em
	    line-height 1.8em
	    li
	      list-style-type none
	
	  .toc-child 
	    margin-left 1em
第一段的toc-article指定了目录整个<div>的背景色、边框色、倒角半径、各种间距以及最大的宽度。注意这里最好指定目录的最大宽度，我将其设为了28%，也就是文章正文那个框的宽度的28%，也可以设为一个固定的长度，比如在笔记本电脑上16em就是个不错的宽度，但为了能适配各种不同尺寸的屏幕，最好还是设置为百分比。如果不指定最大宽度，遇到比较长的标题时，生成的目录会非常难看。这个最大宽度的设置是我在网上其他添加目录的方法中没有见到的。

第二段的toc-title指的就是“文章目录”那四个字，这四个字要比其他字大一些，将其字号设为其他字的120%。

第三段的#toc.toc指定了目录列表的一些细节，将font-size设为0.9em会让目录的字比文章的字稍小一些。最后的.toc-child指定了二级目录的缩进量。

再次生成页面，应该已经可以显示比较美观的目录了。
### 收尾工作

通常情况下我们不需要为每一篇文章都添加目录，因为大部分文章的长度还是相对较短，或者结构简单而没有添加小标题。在我的博客上，需要添加目录的长文还是相对较少的。因为我选择了默认不生成目录，而手动为需要目录的文章添加显式地标记。

下面我就需要编辑每一篇需要添加目录的文章，在文章开头的front-matter中加入toc: true。
## 为Hexo博客的每一篇文章自动追加版权信息
这个需求比较简单，就是希望在每一篇博客的最后追加一段版权声明的文字。我们通过修改博客模板（themes）就可以方便地实现。但是通过修改模板的方式产生的版权信息还是相对独立的，不是文章正文的一部分。这段版权信息存在的主要意义就是防止自动化的工具批量转载博客文章，或许“防止”一词并不恰当，但我们之所以要将版权声明放在正文里，就是希望这些自动化的抓取工具抓取文章时能将版权信息一并抓去。

同时，我们还希望在版权信息中给出这篇文章的永久链接，这样在文章被抓取之后，还会有一个链接指向原文，这样不但可以作为原文被转载的明确证据，同时可以提高原文在搜索引擎中的PageRank。

Hexo博客系统具有良好的可扩展性，我们可以编写一个插件，来实现自动化地为每一篇文章追加版权信息。
### 添加Filter插件
Hexo的插件分为Deployer、Filter、Generator、Renderer、Tag等很多种类。其中Filter插件用于修改一些特定的数据。在Hexo系统内部，已经注册了一类称为before_post_render的Filter插件。这种Filter会在文章正式渲染之前执行，具体的执行和渲染步骤可以参见关于渲染的官方文档。

由于这个功能比较简单，代码量应该也不大，我们不必将其做成一个完整的插件，将其写成一个js脚本，然后放在博客根目录的scripts目录下就可以方便地完成任务。如果你还不了解Script和Plugin的区别，也可以参考关于插件的官方文档。

注册一个before_post_render类型的Filter的代码如下：
	
	hexo.extend.filter.register('before_post_render', function(data){
	    return data;
	});
这样我们就可以在渲染每一篇文章时得到文章内容，并对内容进行修改。Hexo会接收这个Filter的返回值，将其中的内容用于后续的渲染步骤。也就是说在这个函数里对文章内容做出的修改，会最终渲染到输出的HTML代码中。
### 追加版权信息
上文代码中的data其实是一个文章的对象，其中的content字段就代表了文章的源代码（通常是Markdown代码）。我们可以将想要的版权信息追加到这个字段当中，这样这些版权信息就会被送入到后续环节生成HTML代码了。

另外，在博客的某些特定的文章或者页面上，我们可能不想在上面追加版权信息，应该允许用户排除某些特定页面，而在其余的页面上追加版权信息。这个实现起来也很简单，我们可以在不想添加版权信息的页面front-matter中添加一行copyright: false，这个copyright字段也会随着data对象送入Filter，我们可以在代码中判断一下，如果用户确实指定了copyright字段为false，则不追加版权信息。当然copyright这个字段名是我自己起的，你也可以随便用一个自己喜欢的字段名，文中和脚本中保持一致即可。

由于我比较懒，懒到copyright: false都懒得写，由于太懒，所以经常写一些非常短的文章，文章短到比版权信息还要短。这种文章我就不好意思再追加一大串版权信息了，所以我还希望能在文章长度小于50字时自动地不追加版权信息。这个也不难实现，再判断一下文章长度就可以了。
### 追加永久链接
如果版权信息还是给人看的话，那永久链接纯粹就是给机器人看的了。永久链接最好是做成带有链接的URL。这样这个URL不论是否是一个超链接，都可以被搜索引擎捕捉到。同样地，在data对象中也有一个字段表示了文章的永久链接，也就是permalink字段。将这个字段中的URL追加在文章内容之后，后面的Markdown处理器会自动将其处理为一个超链接。
### 代码实现
	// Add a tail to every post from tail.md
	// Great for adding copyright info
	
	var fs = require('fs');
	
	hexo.extend.filter.register('before_post_render', function(data){
	    if(data.copyright == false) return data;
	    var file_content = fs.readFileSync('tail.md');
	    if(file_content && data.content.length > 50) 
	    {
	        data.content += file_content;
	        var permalink = '\n本文永久链接：' + data.permalink;
	        data.content += permalink;
	    }
	    return data;
	});
在具体的代码实现中，我将版权信息保存在了一个名为tail.md的文件当中，在使用时将该文件的内容追加到文章的最后。在读文件时需要注意的是，before_post_render的回调函数是似乎是被同步调用的，也就是说如果函数什么都不返回就结束的话，hexo会直接将未修改的data对象交给后续步骤。所以文件读取操作必须使用同步的fs.readFileSync，如果使用异步的版本，会发现data什么都没有追加，直接执行后续步骤了。

将上述代码保存在一个js文件中，放到博客根目录下的scripts目录中，另外编写一个版权信息的md文件，放在博客根部录下。重新生成博客，应该就可以看到满意的效果了。