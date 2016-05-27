#gradle优化
##gradle优化方法
1. 不用中央仓库。如果你的 repository 配置的是 mavenCentral，放开它吧，全世界的人都在琢磨着怎么虐它，你就不要瞎掺和了。试试 jCenter。

            mavenCentral vs jCenter
            jcenter是世界上最大的Java仓库
            jcenter通过CDN服务，使用的是https协议，安全性更高
            jcenter是mavenCentral的超集，包括许多额外的仓库
            jcenter性能方面比mavenCentral更优
            mavenCentral会自动下载很多与IDE相关的index，而这些用到的少，且不是必需
2. 升级最新的 Gradle 版本。
3. 开启Gradle的电动小马达：gradle.properties

	文件存放位置 ~/.gradle/ ~表示当前用户目录
	
	gradle.properties文件内容如下

	    #如果你的任务没有时序要求，那么打开这个选项可以并发处理多个任务，充分利用硬件资源。
	     org.gradle.parallel=true
	    #这个也可以在命令行通过参数的形式启动，3个小时有效。守护进程可以使编译时间大大缩短
	     org.gradle.daemon=true
	    #这个看需求吧，Gradle 是运行在 Java 虚拟机上的，这个指定了这个虚拟机的堆内存初始化为256M，最大为1G。如果你内存只有2G，那当我没说。
	    org.gradle.jvmargs=-Xms256m -Xmx1024m
