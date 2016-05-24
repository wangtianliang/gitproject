#ubuntu安装wine
1. 对于 64 位系统，需要开启 32 位架构支持
	
		sudo dpkg --add-architecture i386

2. 添加 Wine 官方 PPA
	
		sudo add-apt-repository ppa:wine/wine-builds

3. PPA 添加完成后，我们先刷新包缓存再安装 Wine 1.8：

		sudo apt-get update
		sudo apt-get install --install-recommends winehq-devel

