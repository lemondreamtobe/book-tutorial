# 识别、认证、安全

## 安全HTTP

### 安全HTTP需要提供的功能

- 服务器认证 --- 服务器的可信任性认证
- 客户端认证 --- 客户端的可信任性认证
- 完整性 --- 数据不会被修改
- 加密 --- 客户端与服务器对话是私密的，无需担心被窃听
- 效率 --- 一个运行的足够快的算法，以便底端客户端与服务器使用
- 普适性 --- 基本上所有的客户端和服务器都支持这些协议
- 管理的可扩展性 --- 在任何地方的任何人都可以立即进行安全通信
- 适应性 --- 能够支持当前最知名的安全方法
- 在社会的可行性 --- 满足社会的政治文化需要 

### 什么是HTTPS

`HTTPS`是`HTTP`的安全形式，它在应用层`HTTP`与传输层`TCP`之间添加了一层安全层`SSL/TSL`，所有的`HTTP`请求与响应数据在发送到网络之前，在安全层进行加密

`HTTPS`是在安全的传输层上发送的`HTTP`

HTTPS = HTTP + 证书 + 对称/非对称加密技术

### 什么是密码

`密码`是一套编码方案，一种特殊的报文编码方式和一种稍后使用的相应解码方式的结合体，加密之前的原始报文称为`明文`, 使用密码之后的编码报文成为`密文`

### 什么是密钥

改变密码行为的数字化参数

### 什么是对称密钥加密技术

在编码/解码时使用相同的密钥值的加密算法

`对称密钥加密技术`的缺点之一是接受者与发送者在传送密文之前都要有一个共享的保密密钥

### 什么是公开密钥加密技术

公开密钥加密技术使用两个非对称加密密钥：公开编码密钥与私有解码密钥，大家都可以得到不同的公开密钥，但是可以通过同一解码密钥解码

`公开密钥加密技术`的缺点是公开密钥的加密算法可能会很慢  

一般采用混合加密系统：使用公开密钥加密传递对称加密密钥，使用对称密钥加密需要传输的数据

### RSA

一种 `公开密钥非对称加密系统` 满足就算得到以下所有线索，也无法计算出私有密钥：
- 公开密钥
- 一小片拦截下来的密文
- 一条报文及与之相关的密文

### 数字签名

使用加密系统对报文进行签名（sign），并附加在报文上的特殊加密校验码， 用以说明是谁编写的报文，同时证明报文未篡改过

### 数字证书

因特网上的ID卡，证书（certs）包含了由某个受信任组织担保的用户或公司的相关信息，还包括对象的公开密钥，以及对象和所用算法的描述性信息

- 版本
- 序列号
- 签名算法ID
- 证书颁发者
- 有效期
- 对象名称
- 对象的公开密钥信息
- 发布者唯一的ID
- 对象唯一ID
- 扩展
- 证书的颁发机构签名

### 如何用证书对服务器进行认证

通过`HTTPS`建立一个安全Wen事务后，现代浏览器会自动获取所连接服务器的数字证书，如果没有证书，安全连接失败   
服务器证书中包含不限于以下字段：
- Web站点的名称和主机名
- Web站点的公开密钥
- 签名颁发机构的名称
- 来自签名颁发机构的签名

浏览器预先安装了很多签名颁发机构的证书，如果收到服务器证书，浏览器会对颁发机构的签名进行真实性验证

### 验证站点证书的有效性

1. 日期检测
    > 浏览器检查证书的开始与结束日期，验证是否过期或是否已激活

2. 签名颁发者可信度检测
    >　检测证书是否是由可信任颁发机构颁发的，如果不是则提示一条警告信息给用户，由用户确定是否接受证书

3. 签名检测
    >  一旦判定签名授权是可信的，浏览器就要对签名使用签名颁发机构的公开密钥，并将其与校验码进行比较，验证证书的完整性

4. 站点身份检测
    >  为防止服务器复制他人证书，浏览器会尝试验证证书中的域名与它们对话的服务器的域名是否匹配


### 什么是SSL握手

在发送已加密的HTTP报文之前，客户端与服务器要进行一次SSL握手，在握手过程中，需要完成以下工作：
- 交换协议版本号
- 选择一个两端都了解的密码
- 对两端的身份进行认证
- 生成临时的会话密钥，以便加密信道

SSL握手简化过程： 
1. 客户端发送可供选择的密码并请求证书
2. 服务器发送选中的密码和证书
3. 客户端发送保密信息；客户端和服务器生产密钥
4. 客户端和服务器相互告知，开始加密过程


