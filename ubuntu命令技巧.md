# ubuntu命令技巧

## 清除所有已删除包的残馀配置文件
	dpkg -l |grep ^rc|awk '{print $2}' |sudo xargs dpkg -P 
	如果报如下错误，证明你的系统中没有残留配置文件了，无须担心。
	dpkg: --purge needs at least one package name argument
	Type dpkg --help for help about installing and deinstalling packages [*];
	Use `dselect' or `aptitude' for user-friendly package management;
	Type dpkg -Dhelp for a list of dpkg debug flag values;
	Type dpkg --force-help for a list of forcing options;
	Type dpkg-deb --help for help about manipulating *.deb files;
	Type dpkg --license for copyright license and lack of warranty (GNU GPL) [*].
	Options marked [*] produce a lot of output - pipe it through `less' or `more' !
## 清理旧版本的软件缓存
	sudo apt-get autoclean
## 清理所有软件缓存
	sudo apt-get clean
## 查找文件属于哪个包
	dpkg -S filename
	apt-file search filename
## 查看已经安装了哪些包
	dpkg -l
	dpkg -l | less //翻页查看
## 查询软件xxx依赖哪些包
	apt-cache depends xxx
## 查询软件xxx被哪些包依赖
	apt-cache rdepends xxx
## 查看Ubuntu版本
	lsb_release -a
	或 cat /etc/lsb-release
[转] http://wiki.ubuntu.org.cn/UbuntuSkills
