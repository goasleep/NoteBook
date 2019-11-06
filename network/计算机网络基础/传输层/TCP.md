## TCP协议
特点：
1. 面向连接的传输层协议
2. TCP是点对点的协议
3. TCP提供可靠的交付服务，保证传输的数据无差错、不对事、不重复且有序
4. TCP提供全双工通信
5. TCP是面向字节流的

### TCP报文段
报文段由TCP首部和TCP数据两部分组成
TCP报文首部最短为20字节，最大长度为60字节。
#### 一些重要的字段
1. 序列字段(seq)：序号字段的值为为本报文段所发送的数据的第一个字节的序号
2. 确认号字段(ack)：值为期望收到对方的下一个报文段的数据的第一个字节的序号。若确认号为N，则表示N-1为止的所有数据都正确收到
3. 确认位(ACK)：只有当ACK=1时确认字段才有效
4. 同步位(SYN)：SYN=1表示这是一个连接请求报文或者连接接收报文
5. 推送位(PSH)：当接收到PSH=1时，尽快交付接收应用进程，而不是缓存填满后再交付
6. 终止位(FIN)：用来释放连接，FIN=1表名此报文段的发送方的数据已发送完毕，并要求释放传输连接
7. 检验和：和UDP一样，需要加上12字节的伪首部。协议字段为6，其他和UDP一样

### TCP连接
TPC连接需要解决的问题
1. 要每一方都能够确认对方的存在
2. 要允许双方协商一些参数(如窗口最大值、时间戳等)
3. 能够对运输实体资源进行分配
TCP连接的端口是套接字
TCP采用C/S模式
#### TCP的三次握手
``` mermaid
sequenceDiagram
    Client -> Server:SYN = 1, ACK = 0, seq = x
    Server -> Client:SYN = 1, ACK = 1, seq = y,ack = x + 1
    Client -> Server:ACK = 1, seq = x + 1, ack = y + 1
```
通俗来讲：
client 对 server 说：我要建立连接
server 对 client 说：我已经准好了建立连接了，你也准备一下
client 对 server 说：我也准备好了，可以开始了传输数据了
#### TCP的四次挥手
``` mermaid
sequenceDiagram
    Client -> Server:FIN = 1, seq = u
    Server -> Client:ACK = 1, seq = v,ack = u + 1
    Server -> Client:FIN = 1, ACK = 1, seq = w, ack = u + 1
    Client -> Server:ACK = 1, seq = u + 1, ack = w + 1
    Client -> Client: wait 2MSL(Maximum Segment Lifetime)
```
通俗来讲：
client 对 server 说：我传完数据了，我要关闭链接了
server 对 client 说：等一下，我还有数据传给你
server 传完在对 client 说：我也传完数据了，可以关闭链接了
client 对 server 说：好的，我收到。
client 等了一会再关，为了防止还有消息在路上。如果有通知过来，我就再等会。