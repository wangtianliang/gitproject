docker升级
===

1. 下载docker最近稳定版

		curl -sSL -O https://get.docker.com/builds/Linux/x86_64/docker-1.9.1

2. 停止docker服务并备份文件

		service docker stop
		mv /usr/bin/docker /usr/bin/docker_bak

3. 升级docker

		mv docker-1.9.1 /usr/bin/docker
		chmod +x /usr/bin/docker
		service docker start

4. 查看最新版本

		docker -v