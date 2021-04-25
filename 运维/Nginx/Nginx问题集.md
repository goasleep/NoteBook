## Nginx 如何保证所有worker进程之上的客户端请求数尽量接近。
**使用accept_mutex锁**。accept_mutex是Nginx的负载均衡锁,accept_mutex这把锁可以让多个worker进程轮流地、序列化地与新的客户端建立TCP连接,当某一个worker进程建立的连接数量达到worker_connections配置的最大连接数的7/8时， 会大大地减小该worker进程试图建立新TCP连接的机会， 以此实现所有worker进程之上处理的客户端请求数尽量接近。


## Nginx 如何处理一个HTTP请求
Nginx会取出header头中的Host， 与每个server中的。server_name进行匹配， 以此决定到底由哪一个server块来处理这个请求。

### 匹配优先级
如果Host与多个server块中的server_name都匹配， 这时就会根据匹配优先级来选择实际处理的server块。
匹配优先级：
1. 首先选择所有字符串完全匹配的server_name
2. 其次选择通配符在前面的server_name
3. 再次选择通配符在后面的server_name
4. 最后选择使用正则表达式才匹配的server_name

### 内存分配
Nginx对于每个建立成功的**TCP连接**会预先分配一个内存池.connection_pool_size配置项将指定这个内存池的初始大小，用于减少内核对于小块内存的分配次数。 
Nginx开始处理HTTP请求时， 将会为**每个请求**都分配一个内存池，request_pool_size指定这个内存池的初始大小，用于减少内核对于小块内存的分配次数。 
TCP连接关闭时会销毁connection_pool_size指定的连接内存池， HTTP请求结束时会销毁request_pool_size指定的HTTP请求内存池， 但它们的创建、 销毁时间并不一致， 



## Nginx location
location会尝试根据用户请求中的URI来匹配上面的/uri表达式。location是有顺序的， 当一个请求有可能匹配多个location时， 实际上这个请求会被第一个location处理。

### 匹配规则
1. = 表示把URI作为字符串， 以便与参数中的uri做完全匹配
2. ~ 表示匹配URI时是字母大小写敏感的。
3. ~* 表示匹配URI时忽略字母大小写问题。
4. ^~ 表示匹配URI时只需要其前半部分与uri参数匹配即可。
5. @ 表示仅用于Nginx服务内部请求之间的重定向， 带有@的location不直接处理用户请求


## alisa和root的差别
1. 使用alias时，目录名后面一定要加"/"。
2. alias在使用正则匹配时，必须捕捉要匹配的内容并在指定的内容处使用
3. alias只能位于location块中
4. root的处理结果是：root路径 ＋ location路径，而alisa会使用alias路径替换location路径

## 热点
1. Nginx 事件循环机制
2. Nginx 处理Http请求流程
3. Nginx 如何做热部署