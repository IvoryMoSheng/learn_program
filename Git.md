	$ git config --global user.name "Your Name"           //配置当前用户的账户名
	$ git config --global user.email "email@example.com"  //配置当前用户的邮箱地址
	$ git config --global color.ui true       //配置颜色
	$ git config --global alias.st status      //配置别名

	$ mkdir learngit      //创建目录
	$ cd learngit        //进入目录
	$ pwd                //用于显示当前目录

	$ git init     // 把当前目录变成Git可以管理的仓库
	$ ls -ah         //显示.git

	$  git add readme.txt            //把工作区的文件修改添加到暂存区
	$ git commit -m "wrote a readme file"   //把暂存区的所有内容提交到当前分支，-m参数表示本次提交的说明

	$ git status  //查看仓库当前的状态
	$ git diff readme.txt  //查看修改内容
	$ git diff HEAD -- readme.txt  //查看版本库里面最新版本和工作区的区别

	$ cat readme.txt //显示文本内容
	$ vi readme.txt  //进入文本内容，进行编写
	Esc :wq         //保存文本内容，退出
	$ ls     //显示当前目录下的文件
	$ cd gitskills     //进入指定目录

	$ git log    //显示从最近到最远的的提交日志
	$ git log-1       //显示最近一次的提交
	$ git log --pretty=oneline      //显示从最近到最远的的提交日志 （仅显示版本号）  
	$ git log --graph --pretty=oneline --abbrev-commit // 查看分支合并图
 
	$ git reset --hard HEAD^  //回退到上一版本
	$ git reset --hard commit_id  //回退到指定版本
	$ git reflog     //记录每一次命令 

	$ git checkout -- readme.txt  //撤销工作区的修改，即用版本库里的版本替代工作区的版本

		1. readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
		2. readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态

	$ git reset HEAD readme.txt  //撤销暂存区的修改

	$ rm test.txt   //删除工作区的文件
	$ git rm test.txt //从版本库里删除该文件

	$ ssh-keygen -t rsa -C "youremail@example.com" //创建SSH key
	$ git remote add origin git@github.com:IvoryMoSheng/learngit.git  //本地关联远程库
	$ git push -u origin master  // 把本地库的内容推送到远程，首次需要-u参数表示将本地的master分支与远程的master分支关联起来
	$ git push origin master     //把本地Master分支的最新修改推送到远程库
	$ git clone git@github.com:IvoryMoSheng/gitskills.git    //把远程库克隆到本地库

	$ git checkout -b dev //创建dev分支，然后切换到dev分支，-b参数表示创建并切换
	$ git branch dev  //创建dev分支
	$ git checkout dev  //切换到dev分支
	$ git branch   //查看所有分支，当前分支前面有*号
	$ git merge dev  //用于合并指定分支到当前分支
       Fast-forward //快进模式， 直接把master指向dev的当前提交,删掉分支后，会丢掉分支信息
	$ git branch -d dev     //删除分支
	$ git branch -D feature-vulcan  //强行删除没有合并过的分支
	$ git merge --no-ff -m "merge with no-ff" dev  //--no--ff参数普通合并，表示禁用fast forword

	$ git stash  //隐藏工作现场
	$ git stash list  //查看工作现场
	$ git stash apply  //恢复工作现场
	$ git stash apply stash@{0}  //恢复指定的工作现场
	$ git stash drop  //删除工作现场
	$ git stash pop  //恢复同时删除工作现场

	$ git remote  //查看远程库的信息
	$ git remote -v //显示可以抓取和推送的远程库的地址
	$ git push origin master  //推送主分支
	$ git push origin dev  //推送dev分支

		* master分支是主分支，因此要时刻与远程同步
		* dev分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步
		* bug分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；
		* feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。

	$ git checkout -b dev origin/dev  //创建远程origin的dev分支到本地
	$ git branch --set-upstream dev origin/dev //指定本地dev分支与远程origin/dev分支的链接
	$ git pull //把最新的提交从origin/dev抓下来

	$ git tag v1.0  //打标签
	$ git tag v0.9 commit  id//给指定提交打标签
	$ git tag  //查看所有标签
	$ git show v0.9  //查看标签信息
	$ git tag -a v0.1 -m "version 0.1 released" 3628164   //创建带有说明的标签 用-a指定标签名，-m指定说明文字  
	$ git tag -s v0.2 -m "signed version 0.2 released" fec145a   //用私钥签名一个标签，采用PGP签名， 必须安装gpg（GnuPG）
	$ git tag -d v0.1   //删除本地的标签
	$ git push origin v1.0  //推送指定标签到远程
	$ git push origin --tags //推送全部未推送过的本地标签到远程
	$ git push origin :refs/tags/v0.9   //删除远程的标签

* repository  版本库（仓库）.git
* Working Directory   工作区（工作目录）learngit
* stage(index)  暂存区
* master   主分支，指向提交，可移动
* tag  标签，指向提交，不可移动
* commit   提交
* commit id   版本号
* HEAD  指向表示当前版本的指针 HEAD^表示上一版本  HEAD^^表示上上版本  HEAD~100表示上100个版本
* .gitignore     忽略文件，需要提交到版本库

