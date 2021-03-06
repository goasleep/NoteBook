# DDos
## 简介
DDOS攻击指分布式拒绝服务攻击，即处于不同位置的多个攻击者同时向一个或数个目标发动攻击，或者一个攻击者控制了位于不同位置的多台机器并利用这些机器对受害者同时实施攻击。

## 攻击原理
1. 消耗带宽资源：通过大量请求消耗正常的带宽和协议栈处理资源的能力，从而达到服务端无法正常工作。
2. 耗尽服务器资源：服务器的连接数、cpu数量、提供域名解析的DNS服务器,都属于资源。通过占用服务器的资源，使服务器无法对外提供服务。

## 攻击流程
1. 了解攻击目标：包括不局限于被攻击目标的主机数，地址情况，配置，宽带性能等指标。
2. 攻占傀儡机(肉鸡)：尽量控制多的傀儡机，安装攻击程序。
3. 实施攻击：通过主控机向傀儡机发送攻击指令，实施攻击


## 攻击方式
### 1. 攻击网络宽带资源
   1. 直接攻击
      1. **ICMP/UDP洪水攻击**：攻击者使用受控主机向被攻击目标发送大量的ICMP/IGMP报文，进行洪水攻击以消耗目标的宽带资源
      2. **UDP洪水攻击**：
         1. 小包攻击：小包是指64字节大小的数据包，这是以太网上传输数据帧的最小值，在相同流量下，单包体积越小，数据包的数量就越多。由于交换机、路由器等网络设备需要对没一个数据包进行检查和校验，因此**使用UDP小包攻击能够最有效的增大网络设备处理数据包的压力**，造成处理速度的缓慢和传输延迟等拒绝服务攻击的效果。
         2. 大包攻击：大包是指1500字节以上的数据包，其大小超过了以太网的最大传输单元，**使用UDP大包攻击，能够有效的占用网络接口的传输宽带，并迫使被攻击目标在接受到UDP数据时进行分片重组，造成网络拥堵**，服务器响应速度变慢。
   2. 发射和放大攻击(利用服务器或者路由器多个地方call目标服务器)
        - 发射攻击又被称为DRDoS（分布式反射拒绝服务）攻击，是指**利用路由器、服务器等设施对请求产生应答，从而反射攻击流量并隐藏攻击来源的一种分布式拒绝服务攻击技术**。
        - 放大攻击是一种特殊的反射攻击，**其特殊之处在于反射器对于网络流量具有放大作用**，因此我们也可以将这种反射器成为放大器，进行放大攻击的方式与反射攻击的方式也是基本一致的
      1. **ACK反射攻击**：攻击者利用TCP握手的ACK应答，将SYN的源IP地址伪造成被攻击目标的IP地址，服务器的应答也就会直接发送给被攻击目标。由于使用TCP协议的服务在互联网上广泛存在，**攻击者可以通过受控主机向大量不同的服务器发送伪造源IP地址的SYN请求，从而使服务器响应的大量ACK应答数据涌向被攻击目标**，占用目标的网络宽带资源并拒绝服务。
      2. **DNS放大攻击**：与ACK反射攻击类似，发动DNS放大攻击也需要先进行扫描，以获得大量的开放DNS解析器的地址，并向这些开放DNS解析器发送伪造源地址的查询命令来放大攻击流量
      3. **NTP放大攻击**：NTP(网络时间协议)是用来使计算器时间同步化的一种协议，他可以使计算机与时钟源进行同步化并提供高精准度的时间校正。**与ACK反射攻击和DNS放大攻击类似**，发动NTP放大攻击也需要先进行网络扫描，以获取大量的NTP服务器，并向这些NTP服务器发送伪造源地址的请求来放大攻击流量，**相比于DNS放大攻击，NTP放大攻击的放大倍数更大**，因此其危害也更加严重
      4. **SNMP放大攻击**:SNMP(简单网络管理协议)是目前网络中应用最为广泛的网络管理协议，他提供了一个管理框架来监控和维护互联网的设备.利用SNMP协议中的默认通信字符串和GetBulk请求.**getbulk请求数据包约为60字节，而请求的响应数据能够达到1500字节以上**。攻击者向广泛存在并开启了SNMP服务的网络设备发送getbulk请求，使用默认通信字符串作为认证凭据，并将源IP地址伪造成攻击目标的IP地址，**设备收到getbulk请求后，会将响应结果发送给攻击目标，当大量的响应结果涌向攻击目标时，就会导致攻击目标网络拥堵和缓慢**，造成拒绝服务攻击。
   3. **攻击链路**：攻击者通过traceroute等手段来判断各个僵尸主机和将要攻击的链路之间的位置关系，并根据结果将僵尸主机分为两个部分，然后，**攻击者控制僵尸主机，使其与链路另一侧的每一台僵尸主机进行通信并收发大量数据**，这样，大量的网络数据包就会经过骨干网上的被攻占链路，造成网络拥堵和延时。
### 2. 攻击系统资源
   1. 攻击TCP连接（耗尽TCP连接表，使缓冲区不断清空，强制断开TCP）
      1. **TCP连接洪水攻击**：在三次握手进行的过程中,服务器会创建并保存TCP连接的信息，这个信息通常被保存在连接表结构中，但是，连接表的大小是有限的，一旦服务器接收到的连接数量超过了连接表能存储的数量，**服务器就无法创建新的TCP连接了**
      2. **SYN洪水攻击**: 攻击者利用受控主机发送大量的TCP SYN报文，**使服务器打开大量的半开连接，占满服务器的连接表**，从而影响正常用户与服务器建立会话，造成拒绝服务
      3. **PSH+ACK洪水攻击**:在TCP数据传输的过程中，**PSH标志位来表示当前数据传输结束**。**由于带有PSH标志位的TCP数据包会强制要求接收端将接收缓冲区清空并将数据提交给应用服务进行处理**，因此当攻击者利用受控主机向攻击目标发送大量的PSH+ACK数据包时，**被攻击目标就会消耗大量的系统资源不断地进行接收缓冲区的清空处理**，导致无法正常处理数据，从而造成拒绝服务。
      4. **RST洪水攻击**：**无法正常完成TCP四次握手以终止连接时，就会使用RST报文将连接强制中断**攻击者设法获取客户端的IP地址和端口号，而服务端的IP地址和端口号是已知的。攻击者可以利用RST报文**发送伪造的带有RST标志位的TCP报文，强制中断客户端与服务端的TCP连接**。
      5. **Sockstress攻击(慢速)**：Sockstress攻击首先会完成建立TCP连接后，攻击者将其TCP窗口大小设置为0。攻击目标在传输数据时，发现接收端的TCP窗口大小为0，就会停止传输数据，并发出TCP窗口探测包，询问攻击者其TCP窗口是否有更新，由于攻击者没有更改TCP窗口的大小，被攻击目标就会一直维持TCP连接等待数据发送，并不断进行窗口更新的探测。大量的受控主机进行Sockstress攻击，**被攻击目标会一直维持大量的TCP连接并进行大量窗口更新探测，其TCP连接表会逐渐耗尽，无法连接新的连接而导致拒绝服务**。
   2. 攻击SSL连接（利用SSL解密验证消耗性能）
      1. **THC SSL DOS攻击**：这样的SSL握手过程只需要进行一次即可，但是在SSL协议中有一个Renegotiation选项，通过它可以进行秘钥的重新协商以建立新的秘钥。就是利用Renegotiation选项，造成被攻击目标资源耗尽，在进行SSL连接并握手之后，攻击者反复不断的进行秘钥重新协商过程，**而秘钥重新协商过程需要服务器投入比客户端多15倍的CPU计算资源，攻击者只需要一台普通的台式机就能拖慢一台高性能服务器**，而如果有大量主机同时进行攻击，则会使服务器忙于协商秘钥而完全停止响应
      2. **SSL洪水攻击**：在SSL握手的过程中，服务器会消耗较多的CPU计算资源进行加解密，并进行数据的有效性检验，对于客户端发过来的数据，服务器需要先花费大量的计算资源进行解密，之后才能对数据的有效性进行检验，重要的是，**不论数据是否是有效的，服务器都必须先进行解密才能够做检查，攻击者可以利用这个特性进行SSL洪水攻击**。攻击者并不需要完成SSL握手和秘钥交换，而只需要在这个过程中让服务器去解密和验证，就能够大量的消耗服务器的计算资源
### 3. 攻击应用资源
   1.  攻击DNS服务
       1.  DNS QUERY洪水攻击
       2.  DNS NXDOMAIN洪水攻击
   2.  攻击web服务
       1.  HTTP洪水攻击
       2.  Slowloris攻击（慢速）
       3.  慢速POST请求攻击
       4.  数据处理过程攻击

## 防范措施
### 硬抗
### 流量清洗
流量清洗是通过业务流量进行实时监测，精准识别其中的异常攻击流量，在不影响正常业务的前提下，清洗掉异常流量，实现服务器的流量限流，减轻攻击流量对服务器造成的损害，保证服务正常可用
### CDN


## 参考
https://www.maixj.net/ict/ddos-13728?replytocom=21393
常见攻击方式：https://zhuanlan.zhihu.com/p/30635804
流量清洗原理：https://dun.163.com/news/p/4e52c024c7c94220b3f7201498a388c6