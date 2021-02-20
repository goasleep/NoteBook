# linux启动流程
## linux启动流程（init）
1. 计算机会加载BIOS，BIOS会对自身的硬件做一次健康检查
2. 硬件自检后，就进入引导系统。BIOS默认从硬盘的第0柱面，第0磁道，第一个扇区读取MBR（主引导记录）载入引导程序(如grub)
3. grub会根据配置文件加载kernel镜像，并运行内核加载后的第一个程序/sbin/init，这个文件会根据/etc/inittab 来进行初始化工作
4. 根据/etc/inittab 会确定系统运行级别，初始化并运行/etc/rc.sysinit脚本，该脚本会设置系统变量、网络配置，并启动swap、设定/proc、加载用户自定义模块、记载内核设置等
5. 根据系统运行级别，启动对应的服务，如系统运行级别为3，则会运行/etc/rc3.d/下所有脚本
6. 运行/etc/rc.local/
7. 生成终端或者X windows 等待用户登录

## linux启动流程（systemctl）
https://blog.csdn.net/qq_36119192/article/details/82415113