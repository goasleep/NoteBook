## Docker 资源隔离 借助于Linux 的Namespace
### Namespace是什么
Namespace 是 Linux 内核的一项功能，该功能对内核资源进行分区，以使一组进程看到一组资源，而另一组进程看到另一组资源。
它实现了在同一个主机中，对进程 ID、主机名、用户 ID、文件名、网络和进程间通信等资源的隔离
### Namespace的功能
Linux提供了8种类型的Namespace
|Namespace 名称	|作用|
|----|----|
|Mount（mnt）	|隔离挂载点	|
|Process ID (pid)	|隔离进程 ID	|
|Network (net)	|隔离网络设备，端口号等	|
|Interprocess Communication (ipc)	|隔离 System V IPC 和 POSIX message queues	|
|UTS Namespace(uts)|	隔离主机名和域名	|
|User Namespace (user)|	隔离用户和用户组	|
|Control group (cgroup) Namespace|	隔离 Cgroups 根目录	|
|Time Namespace	|隔离系统时间|	

Docker 使用了前6种Namespace

### 为什么docker需要Namespace
当 Docker 新建一个容器时， 它会创建这六种 Namespace，然后将容器中的进程加入这些 Namespace 之中，使得 Docker 容器中的进程只能看到当前 Namespace 中的系统资源。

正是由于 Docker 使用了 Linux 的这些 Namespace 技术，才实现了 Docker 容器的隔离，可以说没有 Namespace，就没有 Docker 容器

## Docker 资源限制 借助于Linux 的Cgroups
### Cgroups是什么
cgroups（全称：control groups）是 Linux 内核的一个功能，它可以实现限制进程或者进程组的资源（如 CPU、内存、磁盘 IO 等）
### Cgroups功能
1. 资源限制： 限制资源的使用量，例如我们可以通过限制某个业务的内存上限，从而保护主机其他业务的安全运行
2. 优先级控制：不同的组可以有不同的资源（ CPU 、磁盘 IO 等）使用优先级
3. 审计：计算控制组的资源使用情况
4. 控制：控制进程的挂起或恢复

### Cgroups三个核心概念
- 子系统（subsystem）：是一个内核的组件，一个子系统代表一类资源调度控制器。例如内存子系统可以限制内存的使用量，CPU 子系统可以限制 CPU 的使用时间。
- 控制组（cgroup）：表示一组进程和一组带有参数的子系统的关联关系。例如，一个进程使用了 CPU 子系统来限制 CPU 的使用时间，则这个进程和 CPU 子系统的关联关系称为控制组。
- 层级树（hierarchy）：是由一系列的控制组按照树状结构排列组成的。这种排列方式可以使得控制组拥有父子关系，子控制组默认拥有父控制组的属性，也就是子控制组会继承于父控制组

### Docker 是如何使用Cgroups的
Docker 创建容器时，Docker 会根据启动容器的参数，在对应的 cgroups 子系统下创建以容器 ID 为名称的目录, 然后根据容器启动时设置的资源限制参数, 修改对应的 cgroups 子系统资源限制文件, 从而达到资源限制的效果。