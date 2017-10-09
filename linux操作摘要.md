# linux操作摘要
> 本摘要参考资源来自   
>[linux操作系统](http://billie66.github.io/TLCL/book/zh/)   
>[实验楼linux基础课程](https://www.shiyanlou.com/courses/1)

## 常用命令总结
### apt   
>APT由以下的几个主要的命令构成：
>- apt-get
>- apt-cache
>- apt-file

	- apt-cache search <package> 这样系统会列出与<package>名称相匹配的包。
	- apt-get remove [--purge] <package> 移除该软件[及配置文件]
	- apt-get upgrade 所有软件包进行一次升级
	- apt-get dist-upgrade 所有软件包升级并解决依赖关系
	- apt-cache depends <package> 查看软件包的依赖关系
	- apt-get build-dep <package> 安装软件包的编译环境
	- apt-get source <package> 下载软件包的源码(不常用)
	- apt-get check 检查是否有损坏的依赖
	- apt-get -f install 修复依赖关系(适合从deb包安装后修复依赖)

### dpkg
>dpkg常用参数介绍：

	 参数	说明
	 -i	安装指定deb包
	 -R	后面加上目录名，用于安装该目录下的所有deb安装包
	 -r	remove，移除某个已安装的软件包
	 -I	显示deb包文件的信息
	 -s	显示已安装软件的信息
	 -S	搜索已安装的软件包
	 -L	显示已安装软件包的目录信息
	 --force 忽视依赖
	 --instdir  

### 搜索文件命令
>whereis which find locate

-  whereis只能搜索二进制文件(-b)，man帮助文件(-m)和源代码文件(-s)。如果想要获得更全面的搜索结果可以使用locate命令。
- which 搜索是否安装了指定的软件
- locate 通过"/var/lib/mlocate/mlocate.db"数据库查找，
- find 应该是这几个命令中最强大的了，它不但可以通过文件类型、文件名进行查找而且可以根据文件的属性（如文件的时间戳，文件的权限等）进行搜索。[参考博客](https://yq.aliyun.com/articles/52321)

### 进程管理
>进程查看:top ps pstree  
>进程控制

- ps aux : 列出所有进程信息
- pstree : 查看进程的相关性
- top : 实时的查看我们系统的关键一些关键信息的变化已经进程在进程中的实时变化
- kill : kill -signal %jobnumber  
      信号值	作用
      -1	重新读取参数运行，类似与restart
      -2	如同 ctrl+c 的操作退出　
      -9	强制终止该任务　　　
      -15	正常的方式终止该任务

### grep
>它能使用正则表达式搜索文本，并把匹配的行打印出来

	参数	说明
	-b	将二进制文件作为文本来进行匹配
	-c	统计以模式匹配的数目
	-i	忽略大小写
	-n	显示匹配文本所在行的行号
	-v	反选，输出不匹配行的内容
	-r	递归匹配查找
	-A n	n为正整数，表示after的意思，除了列出匹配行之外，还列出后面的n行
	-B n	n为正整数，表示before的意思，除了列出匹配行之外，还列出前面的n行
	--color=auto	将输出中的匹配项设置为自动颜色显示

### tar
	压　缩：tar -jcv -f filename.tar.bz2 要被压缩的文件或目录名称
	查　询：tar -jtv -f filename.tar.bz2
	解压缩：tar -jxv -f filename.tar.bz2 -C 欲解压缩的目录
		 : tar -xaf filename.tar.* (自动匹配解压)

### unzip
	实例 : 将压缩文件text.zip在指定目录/tmp下解压缩，如果已有相同的文件存在，要求unzip命令不覆盖原先的文件。
	 unzip -n test.zip -d /tmp

### 下载命令
>wget curl [参见网络资源](http://man.linuxde.net/curl)

--------
## 常用操作总结
### 源码编译
1. wget下载源码
2. 执行./configure脚本
	(最好在执行make check命令和make clean命令)
3. make
4. make install(如果想卸载通过编译安装的程序只需要在这一步执行make unstall)

### 添加环境变量
>echo "PATH=$PATH:/home/shiyanlou/mybin" >> .bashrc  
>source .bashrc  (注意要在~/目录下操作)

### 用户组操作
 		查看用户:whoami (who -a能打印关于该用户的所有信息)
 		创建用户:sudo adduser username(这个命令还会创建home目录)
 		切换用户: su <username> ; su -<username>附带切换环境变量
		退出当前用户:Ctrl+d
 		查看所属的用户组:groups <username>
 		查看/etc/group文件可看到所有的用户组
 		将其他用户加入到sudo用户组:sudo usermod -G sudo <username>(需要登入sudo组先)
		删除用户:sudo deluser <username>

### 文件权限操作
![文件权限图解](https://dn-anything-about-doc.qbox.me/linux_base/3-10.png/logoblackfont)
![文件权限的二进制编码](https://dn-anything-about-doc.qbox.me/linux_base/3-14.png/logoblackfont)
			变更文件所有者:sudo chown <username> 文件名
			修改文件权限:sudo chmod xxx 文件名
			修改文件夹权限：sudo chmod -R xxx 文件夹

### 添加service启动和开机自启动脚本
参考博客[update-rc.d](http://coderbee.net/index.php/linux/20130524/141)     
复制执行文件到/etc/init.d 或添加一个软链接.

### 硬盘管理操作
>[fdisk 、挂载等基础操作](http://www.cnblogs.com/alylee/p/Linux_disk_management_partition_mount.html)
>[gpt分区操作gdisk](http://blog.csdn.net/fybon/article/details/18516639)

### Ubuntu桌面图标制作
>[.desktop文件编写](http://blog.csdn.net/lu_embedded/article/details/52224442)     

注意：启动图标存储于/usr/share/applications文件夹下
编辑启动图标必须要有：Name,Exec,Icon,Type

## linux目录结构
![linux简明目录结构](https://dn-anything-about-doc.qbox.me/linux_base/4-1.png/logoblackfont)
