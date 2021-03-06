### SSL(Secure Socket Layer)

#### 简介

- 解决问题
  1. 窃听风险，加密机制
  2. 篡改风险，校验机制
  3. 冒充风险，身份证书

- SSL位于应用层和TCP层之间。
- 使用的的算法
  - 密钥交换算法：DH算法(Diffie-Hellman)，RSA加密算法
  - 散列算法：MD5，SHA-1

- 三个特性
  - 保密性
  - 鉴别
  - 完整性

#### SSL的三个子协议

- [握手协议](https://blog.csdn.net/hherima/article/details/52469674)

  1. 建立安全能力：商量SSL版本，交换随机数，选择密码套件（密钥交换算法，加密算法和散列算法）和压缩方法。

  2. 服务器鉴别和密钥交换：客户端校验服务器端发的证书，接收公钥。可能还有一些服务器要求客户进行自身验证的请求。（密钥和证书都使用基础密钥交换方法）

  3. 客户机鉴别与密钥交换：服务器接受客户端使用公钥加密的预备主密钥（client_key_exchange）和协商完成的信息（change cipher sped）。服务器校验客户端发送的证书信息。

  4. 握手完成

     ```sequence
     Client->Server:随机数A，支持的密码套件
     Server->Client:随机数B，选择Client支持的加密算法，服务器证书
     Server->Client:服务器密钥交换
     Client->Client:证书校验
     Client->Server:用server公钥加密预备主密钥，协商信息，证书信息
     Server->Client:握手成功通知
     
     ```

     

     

- [记录协议](https://blog.csdn.net/chengqiuming/article/details/83095673)

  在完成握手协议以后，使用记录协议。记录协议向SSL连接提供两种服务：

  1. 保密性：使用握手协议定义的密钥实现
  2. 完整性：使用握手协议定义的MAC，用于保持消息的完整性

- 警报协议

  客户机和服务器发现错误时，就会向对方发送一个劲爆消息。如果是致命错误，就会关闭SSL链接，删除相关的会话。

  

## 参考文献
https://www.cnblogs.com/sunfb/p/3443221.html