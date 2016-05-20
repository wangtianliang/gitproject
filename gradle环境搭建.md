#Gradle使用
##介绍
Gradle 是什么 Gradle 官方对其描述是：能自动构建、测试、部署、打包、生成静态页面，生成文档等等。Gradle整合了Ant对依赖管理的强大能力、灵活和maven的约定的优于配置的特性形成了一种更有效的构建方式。Gradle基于Groovy的领域定义语言，充满了创新。Gradle已经成为很多开源项目的编译系统的选择。

Gradle的特性 详细的参见其文档。

1. 通过声明来构建和通过约定来构建 task
2. 基于编程（Groovy）来描述语言依赖
3. 构建描述结构化DSL(使得你的构建代码更优雅，更清晰，更易复用)
4. Deep API(提供很多hooks，允许你在构建的任何环节做监控和定制配置)
5. Gradle scales
6. 多工程构建
7. 多种方式管理你的依赖
## Gradle安装
Gradle官网 http://gradle.org/
从Gradle官网下载Gradle安装文件，下载完成之后配置环境变量 方法同jdk
检查gradle是否安装完成：gradle –v 

##	Gradle和Eclipse搭建

* 方法一：http://dist.springsource.com/release/TOOLS/gradle
	
	安装方法：
	Windows --->help--->Install New Software

* 方法二：http://marketplace.eclipse.org/content/gradle-ide-pack

	安装方法：
	打开上边网页拖拽到eclipse中 后续同方法一安装过程
## Eclipse和Gradle配置

Eclipse安装插件gradle之后配置

* 配置Gradle(STS)

	 Windows--->Preferences-->Gradle(STS)

	![配置Gradle(STS)](http://i.imgur.com/lRCG9mH.png)

 	Gradle Distribution folder:配置gradle安装目录

	Gradle User Home directory：自定义文件夹.gradle或者配置成gradle安装目录

* 配置jdk

	展开Gradle(STS) 选择arguments如图所示

	![配置Gradle(STS)--->jdk](http://i.imgur.com/PB1WgJN.png)

	选择右边Workspace JRE：选择所需要的jdk

* 配置Gradle EnIDE

	Windows---> Preferences--->Gradle EnIDE
	![配置Gradle EnIDE](http://i.imgur.com/3Pc6Adc.png)

	Gradle home to use:配置Gradle安装目录

	Alternative JAVA_HOME to use 配置jdk的安装目录
##Gradle项目免提交内容配置

Windows--->Preferences--->Team--->Ignored Resources
![gradle忽略提交部分文件](http://i.imgur.com/lZRWLVi.jpg)

根据项目团队要求配置忽略提交的文件或文件夹：build .gradle 
## 配置项目
	
项目地址：http://103.10.84.37/svn/VIS/VISReportBE/trunk

检出后可自行体验 

项目运行 使用gradle appStart（普通启动） 或者gradle appStartDebug（bug模式启动）

使用gradleappStartDebug启动后需配置远程访问如下图

![](http://i.imgur.com/CoJEanj.jpg)

选择用红线选中的任意一个都可以 
点开之后选择Debug Configurations或者Run Configurations

这边选择的是第一个 走的是Debug Configurations如下图：

![](http://i.imgur.com/a8j7EFl.png)

选择 Remote Java Application右键New 

![](http://i.imgur.com/oxSkvXJ.png)

Name:自定义名字建议和项目同名

Project：选择自己使用的项目

Host：项目所在服务器ip

Port：appStartDebug启动时的端口号 一般为5005