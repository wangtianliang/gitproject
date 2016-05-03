#Linux基本使用
1.安装上传下载命令

 	yum install -y lrzsz 
2.查看端口使用情况

	netstat -ntlp
3.文件归档

	tar -zcvf 目标文件 源文件 例：tar -zcvf /opt/back/file0321.tar.gz  file/
	tar -xzvf 文件  例：tar -xzvf /opt/back/file0321.tar.gz        
4.动态加载日志文件

	tail -fn 500 error.log
5.设置临时别名
	
	alias cdopt='cd /opt/'
6.设置永久别名
	
	编辑.bashrc文件 找到alias在其最后加入
	alias cdopt='cd /opt/'