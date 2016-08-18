Linux修改IP地址DNS服务器等网络设置
===
修改ip地址
---
	vi /etc/sysconfig/network-scripts/ifcfg-eth0　　

	//修改对应网卡的ip地址的配置文件如果你有多个网卡那么ifcfg-eth就有多个，你可以连续按俩次Tab键查看
	# Intel Corporation 82545EM Gigabit Ethernet Controller (Copper)
	DEVICE=eth0    #描述网卡对应的设备别名，例如ifcfg-eth0的文件中它为eth0
	
	BOOTPROTO=static #设置网卡获得ip地址的方式，可能的选项为static，dhcp或bootp，分别对应静态指定的 ip地址，通过dhcp协议获得的ip地址，通过bootp协议获得的ip地址
	
	HWADDR=00:0C:29:0C:B1:00  #（物理地址）对应的网卡物理地址
	
	IPADDR=192.168.2.160  #（IPv4地址）如果设置网卡获得 ip地址的方式为静态指定，此字段就指定了网卡对应的ip地址
	NETMASK=255.255.255.0　　#（子网掩码）网卡对应的网络掩码
	
	ONBOOT=yes #系统启动时是否设置此网络接口，设置为yes时，系统启动时激活此设备
	#（下面的是可以不填写的）
	BROADCAST=192.168.2.255 #对应的子网广播地址
	NETWORK=192.168.2.0　　#（网关）网卡对应的网络地址
  	IPV6INIT=no
  	IPV6_AUTOCONF=no
修改网关
---
	vi /etc/sysconfig/network
  
	NETWORKING=yes #表示系统是否使用IPV4网络，一般设置为yes。如果设为no，则不能使用网络，而且很多系统服务程序将无法启动
	NETWORKING_IPV6=no  #不懂IPV4和IPV6的请百度科普
	HOSTNAME=L160  #设置本机的主机名，这里设置的主机名要和/etc/hosts中设置的主机名对应
	GATEWAY=192.168.2.1  #设置本机连接的网关的IP地址
修改DNS服务器
---
	vi /etc/resolv.conf
	
	#这个域名服务器可以换成你本地的，好处是网络访问要快上那么一点点
	search localdomain
	nameserver 8.8.8.8 #（主）google域名服务器
	nameserver 8.8.4.4 #（从）google域名服务器
重新启动网络配置
---
	service network restart
	/etc/init.d/network restart