---
title: 使用Hexo和Github搭建独立博客之基础搭建
date: 2016-05-03 13:35:41
tags:
categories: Hexo
toc: true
---
#### Hexo的介绍
Hexo是基于node.js的静态博客框架，可以生成静态网页托管在github上

#### 搭建本地Hexo

1.安装[node.js](https://nodejs.org/en/)

2.安装git(需使用到github page搭建)  
下载[msysgit](https://git-for-windows.github.io/)  

3.安装Hexo

在node.js目录下命令行运行代码
	
````
$npm install -g hexo
````

4.部署Hexo  
新建一个文件夹Hexo，命令行运行代码

````
$hexo init	//初始化
$npm install  //安装依赖包
$hexo generate	//生成静态文件  
$hexo server	//启动hexo服务   
````

URL输入localhost:4000进入本地的hexo

#### 将Hexo部署到github pages

1、注册[git](https://github.com/)账号,生成repositories,命名方式为

username.github.io

本地运行GUI->GUI Bash，配置基本信息

````
	$ git config --global user.name "username"
	$ git config --global user.email "email@example.com" 
````

2、配置添加SSH key  
查看本地是否有ssh文件夹（c:/用户/.ssh）  
若没有的话，本地生成ssh钥匙

````
	$ ssh-keygen -t rsa -C "email@example.com"  
````

安装过程中，一直按空格即可  
id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥。

添加SSH公钥到Githug->settings的SSH key中。  
本机测试代码：

````
	$ ssh -T git@github.com
````
出现successfully表示配置成功
3.用[notepad++](http://pan.baidu.com/s/1o8MnDkm)设置hexo配置文件(hexo/_config.yml) 
```` 
	deploy:
	  type: git
	  repo: git@github.com:username/username.github.io.git
	  branch: master
````
4.hexo 部署到github
````
	hexo generate //生成静态文件	
	hexo deploy //部署	
````
---
#### 发表文章
````
	hexo new "postname"
````
在/hexo/source/_posts中打开这个文件（推荐[Markdown](http://pan.baidu.com/s/1eSHeqqA)），配置front-matter
````
	---	
	title: postname 不出现在URL中，可以修改
	date: 2016-05-01 12:11:04 #文章发表日期，可以修改
	categories: hexo #文章文类，可以为空
	tags: hexo #文章标签，可以为空,多标签格式[tag1,tag2]
	---
	#正文
````
#### tip:
##### 关于命令缩写
````
$hexo generate -> $hexo g
$hexo deploy -> $hexo d
#可以合并为
$hexo d -g

$hexo server -> $hexo s
#可以合并为
$hexo s -g
````
##### 关于新建文章
````
hexo new [layout] “postname”
````
1. 可选参数layout，默认值为post。所有参数放置在scaffolds目录下
2. 如果postname包含空格，必须使用"post name"即双引号格式,postname可以为中文，且会出现在URL中

#### bug：
##### 情况：运行hexo d出现“error deployer not found:git”

方案：  
1. 将Hexo/_config.yml的deploy的type的github需要改成git  
2. 运行
````
	npm install hexo-deployer-git --save 
````
3. Hexo d进行部署

##### 情况：404错误"There isn't a GitHub Pages site here."
方案：
生成repositories的username.github.io的username应与Github注册用户昵称一致
##### 情况：当修改文章tag或内容，不能正确重新生成内容，
方案：
1. 可以删除hexo\db.json后重试
2. 若失败，则到public目录删除对应的文件，重新生成

---