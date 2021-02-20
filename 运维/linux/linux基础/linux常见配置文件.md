## 启动时调用的配置文件
1. /etc/inittab:系统初始化配置
2. /etc/rcX.d：系统运行级别
3. /etc/profile：系统级的环境变量和启动程序


## 用户配置
1. /etc/passwd:保存账号等信息
2. /etc/shadow:保存密码等信息，只有root用户能访问
3. /etc/group:用户组

## 文件系统
1. /etc/fstab：挂载配置

## 网络配置
1. /etc/sysconfig/network-scripts/:网络配置(redhat和centos)
2. /etc/hosts:host配置
3. /etc/resolv.conf:DNS客户端配置文件

## other
1. /etc/crontab:定时任务
