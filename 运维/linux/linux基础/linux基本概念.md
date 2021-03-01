## Linux逻辑卷
1. 物理卷（physical volume,PV）：物理磁盘分区
2. 卷组（Volume Group，VG）：PV的集合
3. 逻辑卷（Logic Volume,LV）:PV划出来的一块逻辑磁盘

## Shell 内建命令
指的是Bash本身提供的命令，而不是文件系统中的执行文件，如cd。
执行外建命令会触发IO，还需要fork一个单独的进程来完成，执行完再退出，而内建命令不需要，因此内建命令会比外建命令执行地快

<<<<<<< HEAD

## AWK教程
http://www.ruanyifeng.com/blog/2018/11/awk.html
=======
## 文件标识符
- 标准输入为0
- 标准输出为1
- 标准错误输出为2
>>>>>>> c550d5d6dc72f73111671dced97f4641cb3a7b88
