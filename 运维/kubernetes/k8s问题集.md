## 常见缩写
rc：replication controller
po：pods
svc：service
ns：namespace

## minikube 的安装与设置
https://www.jianshu.com/p/3152aa738e39

## 国内安装

例如下面的命令 kubectl create deployment hello-minikube --image=k8s.gcr.io/echoserver:1.10 ，替换后为 kubectl create deployment hello-minikube --image=registry.aliyuncs.com/google_containers/echoserver:1.10 即可
https://juejin.cn/post/6844904073054027789

kubectl create deployment balanced --image=k8s.gcr.io/echoserver:1.4  

## 为什么要使用service

## replication Controller 和replication Sets的区别与关系

