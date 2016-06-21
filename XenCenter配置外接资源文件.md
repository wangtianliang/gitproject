#XenCenter添加ISO镜像库
安装好XenServer后需要在上面安装我们的虚拟机，这就需要用到’ISO‘镜像文件，在XenCenter下是不能像VMware vSphere Client那样直接挂载我们电脑中的ISO文件，而是需要用到我们的共享文件夹。

1. 创建一个共享文件夹

	在网络中的一台电脑上新建一个文件夹（文件名不能用中文），点击右键–属性–切换到 ‘共享’选项卡–高级共享–确定
	
	![创建共享文件](../images/xencenter1.jpg)
	
	点击密码保护下的‘网络和共享中心’，更改我们当前网络位置的‘密码保护的共享’方式，完后点击确定
	然后把安装系统的ISO文件拷贝到该文件夹中，（注意：共享文件夹内文件的名字不能有中文）
2. 打开XenCenter，连接XenServer

	![连接XenCenter](../images/xencenter2.jpg)
3. 点击‘存储’—新建存储库—选择’Windows文件共享（CIFS）‘—下一步

	![](../images/xencenter3.jpg)
4. 输入ISO库在XenCenter的显示名称，可以保持默认，也可以根据需要自行修改

	![](../images/xencenter4.jpg)

5. 输入刚创建的共享文件夹的路径及用户名密码后点完成

	![](../images/xencenter5.jpg)

6. 创建完成
	现在就可以通过XenCenter查看到我们共享文件夹中的ISO文件了，这里也只能看到ISO文件
	![](../images/xencenter6.jpg)
	 接下来我们就可以创建虚拟机，并用这些ISO文件挂载到光驱来安装操作系统了