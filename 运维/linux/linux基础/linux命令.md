## 账号管理
### 用户管理
1. 新增用户 useradd
```
useradd -u [UID] -g [GID/Group name] -d [home directory] [user name]
useradd -u 5 -g group1 -d /home/group1 username
```
2. 修改密码 passwd
3. 修改用户 usermod
4. 删除用户 userdel

### 组管理
1. 新增用户组 groupadd
2. 删除用户组 groupdel

### 查看用户信息
1. 查看用户：users、who、w
2. 调查用户：finger

### 切换用户
1. 切换成其他用户：su
2. 用其他用户的身份执行命令：sudo

## 定时任务
1. 单一时刻执行一次任务：at
   1. 查看当前at命令调度的任务列表：atq
   2. 删除at任务列表的任务：atrm
2. 周期任务：cron

## 文件管理
### 文件操作
1. 创建文件：touch
2. 删除文件：rm
3. 移动或者重命名文件：mv
4. 查看文件：cat
5. 查看文件头：head(显示文件前10行的内容，使用-n调整显示的行数)
6. 查看文件尾：tail(显示文件后10行内容)
7. 文件格式转换：dos2unix

### 目录操作
1. 进入目录：cd
2. 创建目录：mkdir
3. 删除目录：rm和rmdir
4. 文件和目录复制：cp

### 文件和目录权限
1. 查看文件和目录权限： ls -l
2. 改变文件权限：chmod
3. 改变文件的拥有者：chown
4. 改变文件的拥有组：chgrp
5. 查看文件类型：file
6. 查看文件隐藏属性：lsattr
7. 设置文件隐藏属性：chattr

### 文件查找
1. 一般查找：find
2. 数据库查找：locate
   1. 更新数据库：updatedb
3. 查找执行文件：which/whereis

### 文件打包和压缩
1. gzip/gunzip：压缩成gz
2. tar：压缩成gz/tgz
``` shell
压缩：
tar -zcvf [compressed file name] [origin file name/directory]
tar -zcvf boot.tgz /boot
-z:使用gzip雅座
-c:创建压缩文件
-v:显示当前被压缩的文件
-f:使用文件名

解压：
tar -zxvf [compressed file name] [target directory]
``` 
3. bzip2：压缩成bz2
``` shell
压缩：bzip2 [file name]
解压：bzip -d [compressed file name]
```
4. cpio：通常和find一起使用，通过管道的方式传递给cpio进行备份，生成cpio文件
``` shell
备份：find . -name *.conf | cpio -cov > /temp/config.cpio
还原：cpio --absolute-filenames -icvu < /temp/conf.cpio
```

## 文件系统
### 磁盘挂载
1. 创建文件系统：fdisk
2. 磁盘挂载：mount
3. 磁盘检查：fsck、badblocks
   1. fsck(file system check)用于未挂载的磁盘，否则会造成文件系统损坏
   2. badblocks用于检查磁盘坏道

### 逻辑卷
1. 创建和查看物理卷：pvcreate，pvdisplay
2. 创建和查看卷组：vgcreate，vgdisplay
3. 扩展卷组：vgextend
4. 创建和查看逻辑卷：lvcreate，lvdisplay

## 字符处理
1. 文本搜索：grep
``` shell
grep [-ivnc] [pattern] [file name]
grep -ivnc 'name' test.txt
-i:不区分大小写
-v:反向匹配
-n:输出行号
-c:统计包含匹配的行数
```
2. 排序：sort
``` shell
sort [-ntkr] [file name]
-n:采取数字排序
-t:指定分隔符
-k:指定第几列
-r:反向排序
``` 
3. 删除重复内容：uniq(需要和sort一起使用)
``` shell
uniq [-ic]
-i:忽略大小写
-c:计算重复行数
``` 
4. 截取文本:cut(处理的对象时一行文本)
5. 文本替换:tr
6. 文本合并:paste
7. 分割大文件:split(只支持行数分割和大小分割，二进制文件只能按照大小分割)

## 网络管理
1. 检查和配置网卡：ipconfig
2. 路由和网关：route
3. 网络测试工具
   1. 检测可达性：ping
   2. 查询DNS记录：host
   3. 查询路由：traceroute

## 进程管理
1. 进程查看：ps，top
2. 进程终止：kill，killall
3. 查询进程打开的文件：lsof（list open file）
   1. 查找使用某个端口的进程：lsof -i:8080
   2. 还能恢复文件，只能正在被某个进程使用的文件
4. 进程优先级调整：nice、renice

