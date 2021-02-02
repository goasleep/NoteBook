# Docker 监控
## 使用 docker stats 命令
docker stats命令可以很方便地看到主机上所有容器的 CPU、内存、网络 IO、磁盘 IO、PID 等资源的使用情况
## cAdvisor
cAdvisor 是谷歌开源的一款通用的容器监控解决方案。cAdvisor 不仅可以采集机器上所有运行的容器信息，还提供了基础的查询界面和 HTTP 接口，更方便与外部系统结合。所以，cAdvisor很快成了容器指标监控最常用组件，并且 Kubernetes 也集成了 cAdvisor 作为容器监控指标的默认工具
cAdvisor 监控容器具有以下特点：
1. 可以同时采集物理机和容器的状态
2. 可以展示监控历史数据

## 监控原理
Docker 是基于 Namespace、Cgroups 和联合文件系统实现的
Cgroups 不仅可以用于容器资源的限制，还可以提供容器的资源使用率。无论何种监控方案的实现，底层数据都来源于 Cgroups。
Cgroups 的工作目录为/sys/fs/cgroup



