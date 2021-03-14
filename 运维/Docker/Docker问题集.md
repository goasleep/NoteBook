### Dockerfile 和 docker-compose.yml 的区别
Dockerfile: Dockerfile 是拿来构建自定义镜像的，并没有直接生成容器
docker-compose.yml是用来编排项目的，里面包含使用各种镜像创建的容器服务,在服务启动的时候用到


### 为什么容器是单进程模型

容器只是通过Linux的Namespaces、Cgroups实现了进程级别的隔离。虽然在容器里看不见宿主机上的其他进程，但归根结底它还只是一个运行在宿主机上的进程，所以就不具备操作系统的进程管理能力。

容器的"单进程模型"，并不是指容器里只能运行"一个"进程，而是指容器没有管理多个进程的能力。这是因为容器里的主进程（PID=1 的进程）就是应用本身，其他的进程都是这个主进程的子进程。可是，用户编写的应用，并不能够像正常操作系统里的init进程或者systemd 那样拥有进程管理的功能。
reference：https://cloud.tencent.com/developer/article/1671554