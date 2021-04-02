## 常见资源缩写
rc：replication controller
rs：replicaSet
po：pods
svc：service
ns：namespace
ds: daemonSet
pv: persistent volume
pvc：persistent volume claim
sc：storage class
cm: configMap

## 常见操作
操作资源： kubectl get/delete po
查看yaml属性：kubectl explain pod.spec

## minikube 的安装与设置
https://www.jianshu.com/p/3152aa738e39

## 国内安装

例如下面的命令 kubectl create deployment hello-minikube --image=k8s.gcr.io/echoserver:1.10 ，替换后为 kubectl create deployment hello-minikube --image=registry.aliyuncs.com/google_containers/echoserver:1.10 即可
https://juejin.cn/post/6844904073054027789

kubectl create deployment balanced --image=k8s.gcr.io/echoserver:1.4  

## 为什么要使用service

## ReplicationController 和ReplicationSet的区别与关系
两者的行为完全相同，但是ReplicationSet的标签表达能力更强。ReplicationController的标签选择器只允许包含某个标签的匹配pod。
ReplicationSet的标签选择器还允许匹配缺少某个标签的pod，或包含特定标签名的pod。


## 为什么要使用Downward API将元数据与数据分离

因为这样设计简单元数据需要一直在线，如果分到不同的datanode里面可靠性比较难做，而集中到namenode里面就只需要对namenode做热备份就行。元数据操作之间需要同步，放一台机器上好做，分到不同机器的话就需要做分布式transaction元数据本身并不大，假设每个block 64MB，相应的元数据64B，那么存1PB数据也就需要1GB的元数据。这个数据量放到一台机器上完全没问题。

## 持久卷和持久卷声明是如何匹配的

