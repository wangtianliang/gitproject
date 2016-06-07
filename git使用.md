#git使用
1.使用git push/pull时，避免每次输入用户名密码
使用git bash具体操作如下

	 cd C:\Users\Administrator
	 touch .git-credentials
	 vim .git-credentials
	 add content:https://{username}:{password}@github.com
	 git config --global credential.helper store

2.提交github上

     git push -u origin master
3.GitHub使用教程for Eclipse

	[http://www.cnblogs.com/yc-755909659/p/3753626.html](http://www.cnblogs.com/yc-755909659/p/3753626.html "GitHub使用教程for Eclipse")
4.创建一个资源库并同步到github

    echo "# VISReportBE" >> README.md
    git init
    git add README.md
    git commit -m "first commit"
    git remote add origin https://github.com/wangtianliang/VISReportBE.git
    git push -u origin master
5.删除资源库文件

	 找到setting
	 进入页面后，点击Delete this repository 
	 输入项目名，点击 I understand the consequences，delete this repository
6.修改远程仓库地址 modify remote url
	
	 git remote set-url origin 新地址
7.git提交冲突解决
	
	如果系统中有一些配置文件在服务器上做了配置修改,然后后续开发又新添加一些配置项的时候,在发布这个配置文件的时候,会发生代码冲突:
	error: Your local changes to the following files would be overwritten by merge:
        protected/config/add.md
	Please, commit your changes or stash them before you can merge.
	如果希望保留生产服务器上所做的改动,仅仅并入新配置项, 处理方法如下:
	git stash
	git pull
	git stash pop
	然后可以使用Git diff -w +文件名 来确认代码自动合并的情况.
	
	反过来,如果希望用代码库中的文件完全覆盖本地工作版本. 方法如下:
	git reset --hard
	git pull
	其中git reset是针对版本,如果想针对文件回退本地修改,使用
	git checkout HEAD file/to/restore
8.退出git log
	
		q 回车即退出