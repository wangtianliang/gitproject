#查看容器进程信息

	docker top contianer-id/contianer-name

#进入容器诊断问题
	
	docker exec -ti contianer-id/contianer-name sh/bash

#查看容器性能信息

	docker stats contianer-id/contianer-name

#查看容器配置信息和运行时状态

	docekr inspect contianer-id/contianer-name

#修改docker容器随docker服务启动

	docker update --restart=always contianer-id/contianer-name

#docekr运行后报错
	IPv4 forwarding is disabled. Networking will not work.

	解决方法：
	vi /etc/sysctl.conf
	添加如下代码：

    net.ipv4.ip_forward=1
	重启network服务
	systemctl restart network
 
	查看是否修改成功
	sysctl net.ipv4.ip_forward

	$ sysctl net.ipv4.ip_forward
	net.ipv4.ip_forward = 1

#设置docker容器时区

利用docker来部署服务，经常遇到的一个问题是如何解决容器内的时区问题.

假设现在启动的镜像是tomcat:8.0.35-jre8

	/*直接用宿主机器上的时区默认覆盖容器内的时区配置文件即可，也就是跟宿主机器同样的时区配置  */
	# docker run -v /etc/localtime:/etc/localtime:ro --name=tomcat tomcat:8.0.35-jre8

但是我相信如果写过java的人仍然发现通过java 中new Date()获取到的仍然是容器默认的时区，而是宿主机器上的时区配置，因为java是通过获取timezone来设置时间的。不废话，继续看以下命令:

	/* 这里配置的环境变量 Asia/Shanghai就是我所需要的时区 */
	# docker run -e TZ="Asia/Shanghai" -v /etc/localtime:/etc/localtime:ro --name=tomcat tomcat:8.0.35-jre8

通过这样的启动方式，就是OK了。当然聪明人肯定不会自己每次都在启动的时候加这些配置，当然在基础镜像里面搞好咯。

#docekr容器时区修改

docker container默认是UTC时间的，如果要使用北京时间需要修改时区，有以下几种方式：

* 使用dpkg-reconfigure命令

		$ docker run -i -t ubuntu bash
		root@1f8ccb4c3dc1:/# date
		Wed Sep 10 16:02:38 UTC 2016

		root@1f8ccb4c3dc1:/# dpkg-reconfigure tzdata
		
		Current default time zone: 'Asia/Shanghai'
		Local time is now:      Thu Sep 11 00:02:50 CST 2016.
		Universal Time is now:  Wed Sep 10 16:02:50 UTC 2016.
		
		root@1f8ccb4c3dc1:/# date
		Thu Sep 11 00:02:52 CST 2016
		root@1f8ccb4c3dc1:/# 

* 挂载使用系统/etc/localtime

		$ docker run -i -t -v /etc/localtime:/etc/localtime ubuntu bash
		root@6213cd50d722:/# date
		Thu Sep 11 00:08:56 CST 2016
		root@6213cd50d722:/#
		旧版本的dockere可能文件是/etc/localtime:ro，需要修改挂载方式为：-v /etc/localtime:/etc/localtime:ro

* 直接覆盖/etc/localtime

		$ docker run -i -t ubuntu bash
		root@d4b926fb2c75:/# date
		Wed Sep 10 16:11:15 UTC 2016
		root@d4b926fb2c75:/# apt-get install -y wget > /dev/null 2>&1
		root@d4b926fb2c75:/# wget http://ma6174.u.qiniudn.com/localtime -O /etc/localtime -o /dev/null
		root@d4b926fb2c75:/# date
		Thu Sep 11 00:13:05 CST 2016
		root@d4b926fb2c75:/#