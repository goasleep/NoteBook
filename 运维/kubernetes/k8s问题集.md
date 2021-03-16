## 常见缩写
rc：replication controller
rs：replicaSet
po：pods
svc：service
ns：namespace
ds: daemonSet

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


