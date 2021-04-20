## 配置语法：
1. 配置文件由指令和指令块构成
2. 每条指令以; 解为，指令与参数之前用空格分割
3. 指令块以{}大括号将多条指令组织在一起
4. include语句允许组合多个配置文件以提升可维护性
5. 使用#符号添加注释，提高可读性
6. 使用$符号使用变量
7. 部分指令的参数支持正则表达式


## 优化性能的配置项
1. worker进程个数：worker_processes number
2. worker进程绑定指定CPU：worker_cpu_affinity cpumask[cpumask...(0001)]
3. SSL硬件加速：ssl_engine device
4. 系统调用gettimeofday的执行频率[^1]:timer_resolution t
5. worker进程优先级：worker_priority nice



## 事件类配置项
1. 是否打开accept锁：accept_mutex[on|off][^2]
2. accept锁后到真正建立连接之间的延迟时间：accept_mutex_delay 500ms
3. 批量建立新连接：multi_accept[on|off]
4. 选择事件模型：use[kqueue|rtsig|epoll|/dev/poll|select|poll|eventport] [^3]
5. 每个worker的最大连接数:worker_connections number


## 请求转发配置
### 配置块 server
1. 监听端口
2. 主机名称：server_name name[...]
3. service name散列桶的大小[^4]：server_names_hash_bucket_size
4. service name散列的大小：server_names_hash_max_size
5. 重定向主机名称的处理：server_name_in_redirect on|off
6. Location:

## 内存及磁盘资源的分配配置
1. HTTP包体只存储到磁盘文件中：client_body_in_file_only on|clean|off;
2. HTTP包体尽量写入到一个内存buffer中[^5]：client_body_in_single_buffer on|off;
3. 存储HTTP头部的内存buffer大小：client_header_buffer_size size
4. 存储超大HTTP头部的内存buffer大小[^6]：large_client_header_buffers number size
5. 存储HTTP包体的内存buffer大小[^7]：client_body_buffer_size 8k/16k
6.  HTTP包体的临时存放目录
7.  connection_pool_size
8.  request_pool_size

## 网络连接设置
1. 读取HTTP头部的超时时间：client_header_timeout time
2. 读取HTTP包体的超时时间：client_body_timeout time
3. 发送响应的超时时间：send_timeout time
4. reset_timeout_connection[^8]：reset_timeout_connection on|off
5. lingering_close[^9]：lingering_close off|on|always
6. lingering_timeout
7. lingering_time
8. 对某些浏览器禁用keepalive功能:keepalive_disable[msie6|safari|none]
9. keepalive超时时间:keepalive_timeout time
10. 一个keepalive长连接上允许承载的请求最大数:keepalive_requests n
11. 确定对keepalive连接是否使用TCP_NODELAY选项:tcp_nodelay on|off
12. 按HTTP方法名限制用户请求:limit_except method...{...}
13. HTTP请求包体的最大值:client_max_body_size size
14.  对请求的限速:limit_rate speed
15.  limit_rate_after:Nginx向客户端发送的响应长度超过limit_rate_after后才开始限速

## 文件操作设置
1. sendfile系统调用[^10]：sendfile on|off;
2. AIO系统调用[^11]:aio on|off;
3. directio[^12]：directio size|off;
4. directio对齐：directio_alignment size
5. 打开文件缓存：open_file_cache max=N[inactive=time]|off;
6. 是否缓存打开文件错误的信息：open_file_cache_errors on|off;
7. 不被淘汰的最小访问次数：open_file_cache_min_uses number;
8. 检验缓存中元素有效性的频率：open_file_cache_valid time;

## 客户端请求的特殊处理
1. 忽略不合法的HTTP头部：ignore_invalid_headers on|off
2. HTTP头部是否允许下划线：underscores_in_headers on|off;
3. 对If-Modified-Since头部的处理策略[^13]：if_modified_since[off|exact|before]
4. 文件未找到时是否记录到error日志:log_not_found on|off;
5. 是否合并相邻的“/”：merge_slashes on|off;
6. 设置DNS名字解析服务器的地址：resolver address...;
7. DNS解析的超时时间：resolver_timeout time;
8. 是否在响应的Server头部中标明Nginx版本：server_tokens on|off;



[^1]:gettimeofday:每次内核的事件调用（如epoll、 select、 poll、 kqueue等） 返回时， 都会执行一次gettimeofday，实现用内核的时钟来更新Nginx中的缓存时钟
[^2]:accept_mutex是Nginx的负载均衡锁,ccept_mutex这把锁可以让多个worker进程轮流地、序列化地与新的客户端建立TCP连接。
[^3]:Nginx会自动使用最适合的事件模型
[^4]:server name是存储在散列表里的
[^5]:如果HTTP包体超过了client_header_buffer_size的大小，包体还是会写入到磁盘文件
[^6]:如果HTTP请求行的大小超过配置值，则返回"Request URI too large"(414)
[^7]:HTTP包体会先接收到指定的这块缓存中， 之后才决定是否写入磁盘
[^8]:连接超时后将通过向客户端发送RST包来直接重置连接。 这个选项打开后， Nginx会在某个连接超时后， 不是使用正常情形下的四次握手关闭TCP连接， 而是直接向用户发送RST重置包， 不再等待用户的应答， 直接释放Nginx服务器上关于这个套接字使用的所有缓存.一般关闭
[^9]:该配置控制Nginx关闭用户连接的方式。 always表示关闭用户连接前必须无条件地处理连接上所有用户发送的数据。 off表示关闭连接时完全不管连接上是否已经有准备就绪的来自用户的数据。 on是中间值， 一般情况下在关闭连接前都会处理连接上的用户发送的数据
[^10]:启用Linux上的sendfile系统调用来发送文件， 它减少了内核态与用户态之间的两次内存复制， 这样就会从磁盘中读取文件后直接在内核态发送到网卡设备
[^11]:表示是否在FreeBSD或Linux系统上启用内核级别的异步文件I/O功能,与sendfile功能是互斥的
[^12]:在FreeBSD和Linux系统上使用O_DIRECT选项去读取文件， 缓冲区大小为size，通常对大文件的读取速度有优化作用。与sendfile功能是互斥的。
[^13]:Web浏览器一般会在客户端本地缓存一些文件，并存储当时获取的时
间。 这样，下次向Web服务器获取缓存过的资源时， 就可以用If-Modified-Since头部把上次获取的时间捎带上， 而if_modified_since将根据后面的参数决定如何处理If-Modified-Since头部.