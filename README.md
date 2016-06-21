#Linux基本使用
1. 安装上传下载命令

 		yum install -y lrzsz 
2. 查看端口使用情况

		netstat -ntlp
3. 文件归档

		tar -zcvf 目标文件 源文件 例：tar -zcvf /opt/back/file0321.tar.gz  file/
		tar -xzvf 文件  例：tar -xzvf /opt/back/file0321.tar.gz        
4. 动态加载日志文件

		tail -fn 500 error.log
5. 设置临时别名
	
		alias cdopt='cd /opt/'
6. 设置永久别名
	
		编辑.bashrc文件 找到alias在其最后加入
		alias cdopt='cd /opt/'
7. liunx开启和关闭ping操作
	
		默认开启
		关闭：echo 1 > /proc/sys/net/ipv4/icmp_echo_ignore_all
		开启：echo 0 > /proc/sys/net/ipv4/icmp_echo_ignore_all
8. 杀掉80端口相关的进程
	
		lsof -i :80|grep -v "ID"|awk '{print "kill -9",$2}'|sh
9. 更改ssh默认端口、禁止root登录
	
		vi /etc/ssh/sshd_config
		#添加下面内容
		Port 10022
		Protocol 2
		PermitRootLogin no
		#重启ssh服务
		service sshd reload
10. 创建普通用户并赋予ROOT权限
		
		# 创建一个名为chris的用户
		adduser wtl
		# 给chris创建登录密码
		passwd wtl
		#使用vi打开了sudoers文件
		visudo
		#在sudoers的最后一行加入
		wtl    ALL=(ALL)       ALL
		#保存退出
11. linux同步时间centos
	
		# 安装ntp服务的软件包
		sudo yum install ntp
		# 将ntp服务设置为缺省启动
		sudo chkconfig ntp on
		# 修改启动参数，增加-g -x参数，允许ntp服务在系统时间误差较大时也能正常工作
		sudo vi /etc/sysconfig/ntpd
		# 启动ntp服务
		sudo service ntpd restart
		
		# 将系统时区改为上海时间 (亦即CST时区)
		$ ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime	