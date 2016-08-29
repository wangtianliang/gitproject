#XenCenter添加ISO镜像库

##[在XenServer上添加本地存储](http://icitrix.blog.51cto.com/42654/1409861/ "如何将ISO文件上传到XenServer本地存储中")
	
* 创建文件夹
	
		mkdir -p /data/xen/iso
* 建立该is文件夹对应的sr（存储库）成功后会在XenCenter中显示出来
	
		xe sr-createname-label=isotest type=iso device-config:location=/data/xen/iso device-config:legacy_mode=true content-type=iso
* 上传iso文件到/data/xen/iso文件夹中

	**注意：默认XenServer安装时，Root Size默认是4GB，如果你决定将你的ISO文件放到你的XenServer主机中，建议安装XenServer时扩大Root Size的空间，否则容量较大的ISO文件将无法上传。**
* 上传成功后，选中新建的sr：isotest刷新即可看到刚上传的文件 

##配置windows资源文件夹
 安装好XenServer后需要在上面安装我们的虚拟机，这就需要用到’ISO‘镜像文件，在XenCenter下是不能像VMware vSphere Client那样直接挂载我们电脑中的ISO文件，而是需要用到我们的共享文件夹。

* 创建一个共享文件夹

	在网络中的一台电脑上新建一个文件夹（文件名不能用中文），点击右键–属性–切换到 ‘共享’选项卡–高级共享–确定
	
	![创建共享文件](http://i.imgur.com/zW63VKd.jpg)
	
	点击密码保护下的‘网络和共享中心’，更改我们当前网络位置的‘密码保护的共享’方式，完后点击确定
	然后把安装系统的ISO文件拷贝到该文件夹中，（注意：共享文件夹内文件的名字不能有中文）
* 打开XenCenter，连接XenServer

	![连接XenCenter](http://i.imgur.com/4sbLY2i.jpg)
* 点击‘存储’—新建存储库—选择’Windows文件共享（CIFS）‘—下一步

	![](http://i.imgur.com/UtlsHgg.jpg)
* 输入ISO库在XenCenter的显示名称，可以保持默认，也可以根据需要自行修改

	![](http://i.imgur.com/UzAlbHV.jpg)

* 输入刚创建的共享文件夹的路径及用户名密码后点完成

	![](http://i.imgur.com/hR5NnEe.jpg)

* 创建完成
	现在就可以通过XenCenter查看到我们共享文件夹中的ISO文件了，这里也只能看到ISO文件
	![](http://i.imgur.com/V7arlzQ.jpg)
	 接下来我们就可以创建虚拟机，并用这些ISO文件挂载到光驱来安装操作系统了
