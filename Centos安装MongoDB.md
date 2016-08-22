#CentOS安装MongoDB

##环境
>- centos7
>- mongodb3.2.0

##安装

	cd /opt/local
	wget https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-3.2.0.tgz
	tar -xvf mongodb-linux-x86_64-3.2.0.tgz
	mv mongodb-linux-x86_64-3.2.0 mongodb
###配置环境变量
---
	修改/etc/profile, 添加如下内容
	vi /etc/profile
	
	export MONGODB_HOME=/opt/local/mongodb
	export PATH=$MONGODB_HOME/bin:$PATH
	
	source /etc/profile
###查看是否安装成功
---
	mongod -v
##启动
###创建数据库目录

	mkdir -p /data/mongodb
	mkdir -p /data/mongodb/logs
	touch /data/mongodb/logs/mongodb.log

###添加配置文件
	新建mongodb.conf配置文件, 通过这个配置文件进行启动.
	vi /etc/mongo/mongodb.conf
1. 配置文件参数说明:	

		mongodb的参数说明： 	
		--dbpath 数据库路径(数据文件)
		--logpath 日志文件路径
		--master 指定为主机器
		--slave 指定为从机器
		--source 指定主机器的IP地址
		-pologSize 指定日志文件大小不超过64M.因为resync是非常操作量大且耗时，最好通过设置一个足够大的oplogSize来避免resync(默认的 oplog大小是空闲磁盘大小的5%)。
		--logappend 日志文件末尾添加
		--port 启用端口号
		--fork 在后台运行
		--only 指定只复制哪一个数据库
		--slavedelay 指从复制检测的时间间隔
		--auth 是否需要验证权限登录(用户名和密码)
		
	注：mongodb配置文件里面的参数很多，定制特定的需求，请参考官方文档
2. 配置文件内容:

		dbpath=/data/mongodb
		logpath=/data/mongodb/log/mongodb.log
		logappend=true
		port=27017
		fork=true
		##auth = true # 先关闭, 创建好用户在启动
3. 通过配置文件启动:
	
		mongod -f /etc/mongo/mongodb.conf
###详细权限配置

 [MongoDB 3.0 用户创建](http://www.cnblogs.com/zhoujinyi/p/4610050.html)

###配置防火墙
	
	//添加端口
	firewall-cmd --zone=public --add-port=27017/tcp --permanent
	//重启防火墙
	service firewalld restart 
##测试
	使用客户端robomongo创建连接测试
#注意

 我们创建了用户, 这个时候要开启权限启动, 在配置文件中添加auth=true, 然后重启一下