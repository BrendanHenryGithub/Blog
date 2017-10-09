# grub 命令

## grub2 的安装命令
>[grub2引导的u盘制作](https://my.oschina.net/abcfy2/blog/491140)

grub-install --boot-directory=dir(default /boot) /dev/sdb

## grub2 的引导更新命令
grub-mkconfig -o /.../grub.cfg

# grub2的grub.cfg写法
## 1，引导Ubuntu iso
> [引导Ubuntu iso](http://forum.ubuntu.org.cn/viewtopic.php?t=347622)    

或直接在grub命令行界面输入
关键步骤：    
loopback loop (hd0,1)/ubuntu.iso

set root=(loop)

linux /casper/vmlinuz boot=capser iso-scan/filename=/ubuntu.iso

initrd /casper/initrd.lz

boot
## 2.引导winpe iso
>[引导winpe iso](http://www.itdadao.com/articles/c15a543113p0.html)
