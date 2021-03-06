## TCP 可靠传输
使用校验、序号、确认和重传机制来保证可靠传输

### 序号
序号保证数据能够有序提交给应用层

### 确认号
确认好使期望收到对方的下一个报文段的数据的第一个字节的序号。使用累计确认，可以直接告诉缺失的数据段

### 重传
引起重传的原因：超时和冗余ACK
#### 超时
使用一个计时器，在计时器时间内没有收到确认，就会重传该报文
超时使用的是一个自适应算法
往返时间为RTT(Round-Trip-Time)的计算方式
$$ RTT_{new} = (1-\alpha) * RTT_{old} + \alpha * RTT_{样本}  $$
$ \alpha $推荐为0.125
超时计时器的重传事件RTO(Retransmission Time-Out)
$$ RTO = RTT + 4 * RTT_D$$
$RTT_D$是RTT的偏差的加权平均
$$ RTT_D^{new} = (1-\beta) * RTT_D^{old} + \beta *|RTT - RTT_{样本}|$$
$\beta$ 为小于1的系数，推荐值为0.25
#### 冗余ACK（冗余确认）
TCP规定每当一个比期望序号大的失序报文段到达时，就会发送一个冗余的ACK，指明下一个期待字节的序号。
TCP规定当发送方收到对同一个报文段的3个冗余ACK时，就可以认为更在这个被确认报文段之后的报文段已经丢失。

## 定时器
- 超时重传定时器（retransmit）
- 持续定时器（persist）
- 保活定时器（keepalive，这和 HTTP 协议中的 keepalive 不是同一个概念）
- TIME_WAIT 定时器