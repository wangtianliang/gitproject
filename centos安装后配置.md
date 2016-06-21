#centos安装后配置
1. 修改网卡配置
	
		vi /etc/sysconfig/network-scripts/ifcfg-eth0 
		修改ONBOOT=“yes”
		增加IPADDR="192.168.0.90" NETMASK="255.255.255.0"
2. 修改网关
	
		vi /etc/sysconfig/network
		加入GATEWAY=192.168.0.1
3. 修改DNS（可上网配置）
		
		vi /etc/resolv.conf
		加入nameserver:
		nameserver 114.114.114.114
		nameserver 8.8.8.8
4. 重启网络服务
	
		service network restart
5. yum源的配置和使用
	
	[http://www.centoscn.com/CentOS/2015/0918/6186.html](http://www.centoscn.com/CentOS/2015/0918/6186.html "CentOS7下yum源的配置与使用")
6. yum报错的修改

	[http://blog.csdn.net/llnara/article/details/8645846](http://blog.csdn.net/llnara/article/details/8645846 "CentOS yum报错的一般解决方法")

	[http://bbs.vpser.net/archiver/tid-13873.html](http://bbs.vpser.net/archiver/tid-13873.html "修改了/etc/resolv.conf之后还是不行")
7. 系统优化
	
		1. echo "ulimit -SHn 102400" >> /etc/rc.local
		
		2. vi /etc/security/limits.conf 加入：
			*           soft   nofile       65535
			*           hard   nofile       65535
		3. 关闭selinux，如果关闭后ssh连不上则重启服务器
			sed -i 's/SELINUX=enforcing/SELINUX=disabled/' /etc/selinux/config
			或vim /etc/sysconfig/selinux
			# SELINUX=enforcing
			SELINUX=disabled
		4. 关闭部分功能
			chkconfig bluetooth off 
			chkconfig cups off 
			chkconfig ip6tables off
		5. 关闭ipv6
			echo "NETWORKING_IPV6=off" >> /etc/sysconfig/network

