## 无权限连接Docker Daemon socket
问题描述：Got permission denied while trying to connect to the Docker daemon socket
问题原因：docker进程使用Unix Socket而不是TCP端口。而默认情况下，Unix socket属于root用户，需要root权限才能访问
解决措施：
1. 使用sudo获取管理员权限
2. docker守护进程启动时，会默认赋予docker的用户组读写Unix Socket的权限，因此只需将当前用户添加到用户组就有权限访问Unix Socket了
``` shell
sudo groupadd docker     #添加docker用户组
sudo gpasswd -a $USER docker     #将登陆用户加入到docker用户组中
newgrp docker     #更新用户组
docker ps    #测试docker命令是否可以使用sudo正常使用
```

## 修改国内镜像源
问题描述：Error response from daemon: Head "https://registry-1.docker.io/v2/library/ngnix/manifests/latest": Get "https://auth.docker.io/token?scope=repository%3Alibrary%2Fngnix%3Apull&service=registry.docker.io": net/http: TLS handshake timeout.
问题原因：国内无法访问镜像源
解决措施：更改为国内镜像源
1. sudo vim /etc/docker/daemon.json
2. 修改配置文件
``` properties
{
"registry-mirrors": ["https://docker.mirrors.ustc.edu.cn/","https://hub-mirror.c.163.com","https://registry.docker-cn.com"],
"insecure-registries": ["10.0.0.12:5000"]
}
```
3. 重新加载守护进程：sudo systemctl daemon-reload
4. 重启docker：sudo service docker restart