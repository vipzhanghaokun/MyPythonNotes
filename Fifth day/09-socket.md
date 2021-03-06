# socket - 底层网络接口 

##  一、网络知识

### 常见网络协议

http，https，smtp，ftp，ssh，snmp，ICMP，DHCP

### OSI网络七层模型

- 应用层
- 表示层
- 会话层
- 传输层
- 网络层
- 数据链路层
- 物理层

### 三次握手

​	三次握手协议指的是在发送数据的准备阶段，服务器与客户端之间需要进行三次交互。

* 第一次握手：客户端发送syn包到服务器，并进入syn_send状态，等待服务器确认；
* 第二次握手：服务器收到syn包，必须确认客户的syn，同时自己也发送一个syn包，即SYN+ACK包，此时服务器进入SYN_RECV状态；
* 第三次握手：客户端收到服务器的SYN+ACK包，向服务器发送确认包ACK，此包发送完毕，客户端和服务器进入ESTABLISHED状态，完成三次握手。

### 四次挥手

​	四次挥手指的是连接终止协议。

### 网络协议

* **TCP协议：**

  ​TCP是面向连接的通信协议，通过三次握手建立连接，通讯完成时要拆除连接，由于TCP是面向连接的所以只能用于端到端的通讯。

  ​TCP提供的是一种可靠的数据流服务，采用“带重传的肯定确认”技术来实现传输的可靠性。

* **UDP协议：**

  ​UDP是面向无连接的通讯协议，UDP数据包括目的端口号和源端口号信息，由于通讯不需要连接，所以可以实现广播发送。

  ​UDP通讯时不需要接收方确认，属于不可靠的传输，可能会出现丢包现象，实际应用中要求程序员编程验证。



## 二、SOCKET

> ​	socket本质是编程接口(API)，对TCP/IP的封装，TCP/IP也要提供可供程序员做网络开发所用的接口，这就是Socket编程接口

​	IP地址用于确认主机位置，Port用于确认主机中所用的程序。

```
# 接收端
'''
1、导入socket模块

2、选择协议TCP or UDP

3、绑定地址（IP,Port）

4、监听地址

5、等待接入

6、接收数据 / 发送数据

'''


# 发送端
'''
1、导入socket模块

2、选择协议TCP or UDP

3、连接地址（IP+Port）

4、发送数据 / 接收数据

5、关闭连接
'''
```



* socket Families（地址家族）

  AF：（address family）

  **socket.AF_UNIX** : unix本机进程间通信

  **socket.AF_INET** : TPV4

  **socket.AF_INET**6 : IPV6

* socket Types（socket类型）

  socket.SOCK_STREAM：TCP使用的套接字类型

  oscket.SOCK_DGRAM：UDP使用的套接字类型，DGRAM源于（datagrame，数据报）




## 三、创建TCP服务器

​	TCP服务端简单示例：

```python
import socket

s1 = socket.socket()
s1.bind(('127.0.0.1',1200))

s1.listen()
print('等待连接。。。')
conn,addr = s1.accept()    # conn是客户端连接过来，在服务器端为其生成的连接实例。
print('连接来自。。。',addr)

data = conn.recv(1024)
print(data)
conn.send(data.upper())

s1.close()
```

​	TCP客户端简单示例：

```python
import socket

c1 = socket.socket()
c1.connect(('127.0.0.1',1200))

c1.send(b'Hello World!')
data = c1.recv(1024)
print(data)

c1.close()
```

​	注：发送中文字符，需要`encode()`进行编码