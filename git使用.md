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
