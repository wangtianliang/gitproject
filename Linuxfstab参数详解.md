# Linux fstab 参数详解

 Linux 下的加挂硬盘经常使用。 在最后一步修改/etc/fstab 文件设置开机自动挂载。今天用的时候，发现对这个文件中的最后2个参数不是很明白。 再次MAN了一下。
 
		[root@qs-wg-db1 /]# cat /etc/fstab
		LABEL=/          /                       ext3    defaults        1 1
		LABEL=/boot      /boot                   ext3    defaults        1 2
		tmpfs             /dev/shm                tmpfs   defaults        0 0
		devpts            /dev/pts                 devpts  gid=5,mode=620  0 0
		sysfs             /sys                     sysfs   defaults        0 0
		proc             /proc                    proc    defaults        0 0
		LABEL=SWAP-sda2  swap                 swap    defaults        0 0
		/dev/sda1          /u01                   ext3    defaults        0 0
		 
		 
		[root@qs-wg-db1 /]# man fstab
		FSTAB(5)      Linux Programmer's Manual                  FSTAB(5)
		 
		NAME
		       fstab - static information about the filesystems
		SYNOPSIS
		       #include <fstab.h>
		DESCRIPTION
		       The  file  fstab  contains  descriptive information about the various file systems. fstab is only read by programs, and not written; It  is  the  duty  of  the  system administrator  to  properly  create  and  maintain  this  file.  Each filesystem is described on a separate line; fields on each line are separated by tabs or  spaces. Lines  starting  with '#' are comments.  The order of records in fstab is important（fatab中记录的顺序很重要） because fsck(8), mount(8), and umount(8) sequentially iterate through  fstab  doing their thing.
		       The first field（第一个字段）, (fs_spec), describes the block special device or remote filesystem to be mounted.
		       For ordinary mounts it will hold (a link to) a block special device node  (as  created  by  mknod(8)) for the device to be mounted, like '/dev/cdrom' or '/dev/sdb7'.
		       For NFS mounts one will have <host>:<dir>, e.g., 'knuth.aeb.nl:/'.  For procfs, use 'proc'.
		       Instead  of  giving  the  device  explicitly,  one  may  indicate the (ext2 or xfs) filesystem that is to be mounted by its UUID or volume label  (cf.   e2label(8)  or xfs_admin(8)),   writing   LABEL=<label>  or  UUID=<uuid>,  e.g.,  'LABEL=Boot'  or 'UUID=3e6be9de-8139-11d1-9106-a43f08d823a6'.   This  will  make  the  system   more robust:  adding  or  removing  a SCSI disk changes the disk device name but not the filesystem volume label.
		       The second field, (fs_file),（第二个字段） describes the mount point  for  the  filesystem.   For swap partitions, this field should be specified as 'none'. If the name of the mount point contains spaces these can be escaped as '/040'.
		       The third field, (fs_vfstype)（第三个字段）, describes the type of the  filesystem.   Linux  supports lots of filesystem types（支持的文件类型）, such as adfs, affs, autofs, coda, coherent, cramfs, devpts, efs, ext2, ext3, hfs, hpfs, iso9660, jfs, minix, msdos, ncpfs,  nfs,  ntfs, proc,  qnx4,  reiserfs,  romfs,  smbfs, sysv, tmpfs, udf, ufs, umsdos, vfat, xenix, xfs, and possibly others. For more details, see mount(8).  For the filesystems currently  supported  by  the  running  kernel,  see /proc/filesystems.  An entry swap denotes a file or partition to be used  for  swapping,  cf.  swapon(8).   An  entry ignore causes the line to be ignored.  This is useful to show disk partitions which are currently unused.
		 
		       The fourth field, (fs_mntops)（第四个字段）, describes the  mount  options  associated  with  the filesystem.  It  is  formatted  as  a comma separated list of options.  It contains at least the type of mount plus any additional options appropriate to the filesystem type.   For documentation on the available options for non-nfs file systems, see mount(8).  For documentation on all nfs-specific options have a look at nfs(5).   Common  for  all types  of  file  system are the options ''noauto'' (do not mount when "mount -a" is given, e.g., at boot time), ''user'' (allow a  user  to  mount),  ''owner''  (allow device  owner to mount), ''pamconsole'' (allow a user at the console to mount), and ''comment'' (e.g., for use by fstab-maintaining programs).  The  ''owner'',  ''pamconsole''  and  ''comment''  options  are  Linux-specific.   For  more details, see mount(8).
		       The fifth field, (fs_freq),（第五个字段） is used for these filesystems by the dump(8) command to determine  which filesystems need to be dumped.  If the fifth field is not present, a value of zero is returned and dump will assume that the filesystem does not need to be dumped.（0表示不需要dump）
		 
		       The sixth field, (fs_passno)（第六个字段）, is used by the fsck(8) program to determine the order in which filesystem checks are done at reboot time.  The root filesystem should  be specified  with  a fs_passno of 1, and other filesystems should have a fs_passno of 2.  Filesystems within a drive will be checked  sequentially,  but  filesystems  on different  drives will be checked at the same time to utilize parallelism available in the hardware.  If the sixth field is not present or zero, a  value  of  zero  is  returned and fsck will assume that the filesystem does not need to be checked. （如果不指定或者为0， 该硬件在重启时fsck将不检查）
		 
		       The proper way to read records from fstab is to use the routines getmntent(3).
		 
		FILES
		       /etc/fstab
		SEE ALSO
		       getmntent(3), mount(8), swapon(8), fs(5), nfs(5)
		 
		HISTORY
		       The ancestor of this fstab file format appeared in 4.0BSD.
 
 
	网上找到一份中文版的：
	fs_spec　fs_file　fs_type　fs_options　fs_dump　fs_pass　
	/dev/hda1　/　　　ext2　　defaults　　 　1　　　　1　
	 
	（1）fs_spec： 该字段定义希望加载的文件系统所在的设备或远程文件系统，对于一般的本地块设备情况来说：IDE设备一般描述为 /dev/hdaXN，X是IDE 设备通道(a,　b,　or　c)，N代表分区号；SCSI设备一描述为/dev/sdaXN。对于NFS情况，格式一般为:,例如： 'knuth.aeb.nl:/'。对于procfs，使用'proc'来定义。 对文件系统的定义(fs spec)，它描述了将被装载的块设备或远程文件系统。对于通常的mount操作而言，这个字段应该包括一个将被装载的块设备的设备结点(通过mknod 命令来创建)或指向这类结点的连接(例如/dev/cdrom或/dev/sdb)，对于NFS mount操作，这个字段应该包含host:dir格式的信息，例如:knuth.aeb.nl:/，对于进程文件系统procfs，使用proc。
	 
	　　除了显示的使用设备名，你可以使用设备的UUID或设备的卷标签，例如，你可以在这个字段写成“LABAL=root”或“UUID=3e6be9de -8139-11d1-9106-a43f08d823a6”，这将使系统更具伸缩性。例如，如果你的系统添加或移除了一个SCSI硬盘，这有可以改变你的设备名，但它不会修改你的卷标签。
	 
	（2）fs_file： 该字段描述希望的文件系统加载的目录点，对于swap设备，该字段为none；对于加载目录名包含空格的情况，用40来表示空格。描述文件系统的载入点，对于交换分区(swap)，这个字段定义为none，如果在载入点的路径中包含空格符，可以用“/040”来替代空格符。
	 
	（3）fs_type：　定义了该设备上的文件系统，一般常见的文件类型为ext2　(Linux设备的常用文件类型)、vfat(Windows系统的fat32格式)、NTFS、iso9600等.文件系统类型(fs vfstype)，主要用来定义文件系统的类型。Linux系统支持大量的文件类型，包括sdfs，affs，autofs，jfs，minix， msdos, ncpfs, nfs, ntfs, proc, qnx4, reiserfs, romfs,，smbfs, sysv, tmpfs, udf, ufs, umsdos, vfat, xenix, xfs等等。如果想了解你的kernel目前支持哪些文件系统，可以查看/proc/filesystems的内容。如果这个字段定义为swap，这条纪录将关联到一个用于交换目的的文件或分区。如果这个字段定义为ignored，这行将被忽略。这对于显示目前没有使用的分区非常有用。
	　
	（4）fs_options：　指定加载该设备的文件系统是需要使用的特定参数选项，多个参数是由逗号分隔开来。文件系统选项(fs mntops)在装载文件系统时使用的装载选项。多个选项之间用逗号做分隔符，这些选项列表包括了装载类型以及对于该文件系统合适的其它装载选项。对于非 NFS系统可用的装载选项可以参看mount命令的说明，对于nfs系统的选项可以查看关于nfs的文档。对于所有文件系统都适用的选项有noauto (当使用mount –a命令时不载入)，user(允许用户进行装载)，owner(允许设备所有人装载)，_netdev(设备需要网络)，后两个选项是linux系统所特有的。
	 
	对于大多数系统使用"defaults"就可以满足需要。其他常见的选项包括：
	选项　　　　　　　　　　　　　　含义
	ro　　　　以只读模式加载该文件系统
	sync　　　不对该设备的写操作进行缓冲处理，这可以防止在非正常关机时情况下破坏文件系统，但是却降低了计算机速度
	user　　　允许普通用户加载该文件系统
	quota　　　强制在该文件系统上进行磁盘定额限制
	noauto　　不再使用mount　－a命令（例如系统启动时）加载该文件系统
	 
	（5）fs_dump： 该选项被"dump"命令使用来检查一个文件系统应该以多快频率进行转储，若不需要转储就设置该字段为0.文件系统频率(fs_freq)，被dump程序使用来确定哪个文件系统需要dump，如果最后一个字段没有设置，系统将认为其值为0，而dump程序则认为此文件系统无需dump。
	 
	（6）fs_pass： 　该字段被fsck命令用来决定在启动时需要被扫描的文件系统的顺序，根文件系统"/"对应该字段的值应该为1，其他文件系统应该为2。若该文件系统无需在启动时扫描则设置该字段为0.被fsck程序所使用来确定进行在系统重启进行文件系统检查时的顺序，对于根系统/这个值应设为1，其它文件系统可以设为2，在同一个物理硬盘内的文件系统应该被顺序检测，而不同硬盘中的文件系统则应该同时检测以充分利用系统的并行性。如果最后一个字段值为0或没有设置，fsck程序装跳过此文件系统的检测。**