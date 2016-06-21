#在CentOS上安装Docker
转自[https://mos.meituan.com/library/26/how-to-install-docker-on-centos/](https://mos.meituan.com/library/26/how-to-install-docker-on-centos/ "在CentOS上安装Docker")

Docker是一个能够把开发应用程序自动部署到容器的开源引擎。它由Docker公司的团队编写，基于Apache 2.0开源协议授权。它提供了一个简单、轻量的建模方式，使开发生命周期更高效快速，鼓励了面向服务的架构设计。

##前提条件

###内核

Docker运行对内核要求比较高，因此一般建议直接在Ubuntu这样的平台运行。但作为一个容器标准，Docker也是支持其他如CentOS, Mac OS X, Windows等平台。目前Docker支持以下版本CentOS:

>* CentOS 7(64位)
>* CentOS 6.5(64位)及以后

在运行CentOS 6.5及以后版本时，需要内核版本>=2.6.32-431，因为这些内核包含了运行Docker的一些特定修改。

	$ uname -r
	2.6.32-431.17.1.el6.x86_64
###Device Mapper

Docker默认使用AUFS作为存储驱动，但是AUFS并没有被包括在Linux的主线内核中。CentOS中可以使用Device Mapper作为存储驱动，这是在2.6.9内核版本引入的新功能。我们需要先确认是否启用该功能:

	$ ls -l /sys/class/misc/device-mapper
	lrwxrwxrwx 1 root root 0 May  1 20:55 /sys/class/misc/device-mapper -> ../../devices/virtual/misc/device-mapper
如果没有检测到Device Mapper，需要安装device-mapper软件包:

	$ sudo yum install -y device-mapper
然后重新加载dm_mod内核模块:

	$ sudo modprobe dm_mod
##安装

* CentOS 7

Docker RPM包已经包含在CentOS-Extra仓库中，所以我们可以直接使用Yum安装:

	$ sudo yum install docker
注意: 这里我们需要注意FirewallD， 在重启FirewallD之后，需要重启你的Docker Deamon.

* CentOS 6.5

>* 第一步 Enable EPEL

对于CentOS6.5, Docker可以在EPEL源里面找到，所以我们首先需要确保启用EPEL。

	$ sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
>* 第二步 Remove Docker

需要注意的是，CentOS6.5中，已经有一个同名docker的可执行系统程序包。所以Docker RPM包命名为docker-io，我们先卸掉docker。

	$ sudo yum -y remove docker
>* 第三步 Install Docker-IO

最后需要安装docker-io的RPM包。

	$ sudo yum -y install docker-io
这样完成了Docker的安装。

##启动

* CentOS 6.5

>* 第一步 启动服务

一旦安装好Docker之后，我们需要启动Docker Deamon:

	$ sudo service docker start
>* 第二步 设置开机启动(可选)

如果希望Docker Deamon开机运行，还需要做如下操作:

	$ sudo chkconfig docker on
* CentOS 7

以上针对CentOS 6.5的启动步骤同样适用于CentOS 7. 同时CentOS 7中使用Systemd替换了SysV的初始化，我们也可以直接使用Systemd来管理Docker Daemon.

启动过程

	$ sudo systemctl start service
	$ sudo systemctl enable docker  # option
已知BUG

在使用CentOS 7中默认安装的是Docker 1.5.0-28，此版本Docker在启动时会出现错误信息如下:

	/usr/bin/docker: relocation error: /usr/bin/docker: symbol dm_task_get_info_with_deferred_remove, version Base not defined in file libdevmapper.so.1.02 with link time reference
这个BUG是CentOS 7中此版本的Docker软件包在包依赖中没有依赖正确的Device-mapper软件包。这个BUG具体信息可以查看Docker Issue或RedHat Bugzilla。只需要我们进行一次整体的升级即可解决:

	$ sudo yum update
请不要只升级Docker，这样我们就可以按照前面步骤启动Docker Daemon.

##验证

* 验证Docker Deamon

启动服务后，直接用docker info命令确认docker是否正确安装并运行:

	$ sudo docker info
	
	Containers: 0
	Images: 0
	......
* 验证Docker Client

现在就让我们验证下Docker是否能正常运行，首先我们来获取最新的centos镜像:

	$ sudo docker pull centos
这里默认使用的是Docker官方源，不稳定。国内可以使用DaoCloud的Docker加速器服务，但要求Docker版本>=1.3.2。然后我们检查是否能看到镜像:

	$ sudo docker images centos
使用DaoCloud加速器服务比较简单，只需要简单修改配置文件增加registry-mirror即可。编辑文件/etc/sysconfig/docker, 修改OPTIONS为你的加速mirror:

	OPTIONS="--registry-mirror=Your DaoCloud Mirror Address --selinux-enabled"
然后重启Docker Daemon。激动的时刻到了，让我们运行一下:

	$ sudo docker run -i -t centos /bin/bash
一切正常的话，你会看到一个终端提示符，然后你就可以像操作任何CentOS机器一样进行你的体验。

#方法二：
1. 安装docker 
		
		#查看系统内核版本 确保内核在3.0以上
		uname -r
		
		确认当前登录用户是否具有root权限
		
		#确保yum包是最新的
		sudo yum update
		
	1.1 通过yum安装docker
 
		#添加yum源
		sudo tee /etc/yum.repos.d/docker.repo <<-'EOF'
		[dockerrepo]
		name=Docker Repository
		baseurl=https://yum.dockerproject.org/repo/main/centos/$releasever/
		enabled=1
		gpgcheck=1
		gpgkey=https://yum.dockerproject.org/gpg
		EOF
		
		#安装docker
		sudo yum install docker-engine

		#启动docker
		sudo service docker start
	1.2 通过脚本安装
		
		#添加yum源和安装docker
		curl -fsSL https://get.docker.com/ | sh
		#启动docker
		service docker start
2. 添加docker用户组
		
		#创建docker用户组
		sudo groupadd docker
		#添加用户到docker组
		sudo usermod -aG docker your_username
		#退出重新使用上面用户重新登录
3. 卸载docker
		
		#查看当前安装docker
		yum list installed | grep docker
		#卸载docker
		sudo yum -y remove docker-engine.x86_64
		#删除镜像、容器
		rm -rf /var/lib/docker
		#查找并删除用户配置文件