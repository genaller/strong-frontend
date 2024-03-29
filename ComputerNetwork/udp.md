# udp 用户数据报协议
UDP协议全称是用户数据报协议，在网络中它与TCP协议一样用于处理数据包，是一种无连接的协议。

### udp协议的构成
- udp协议首部：UDP 协议会用自己的分组结构封装用户消息，它只增加了 4 个字段：源端口、目标端口、分组长度和校验和。
- UDP 数据报中的 源端口 和 校验和 字段都是可选的。IP 分组的首部也有校验和，应用程序可以忽略 UDP 校验和。

说到底，UDP 仅仅是在 IP 层之上通过嵌入应用程序的
源端口和目标端口，提供了一个“应用程序多路复用”机制。

### udp无服务的解释
- 不保证消息交付
不确认，不重传，无超时。
- 不保证交付顺序
不设置包序号，不重排，不会发生队首阻塞。
- 不跟踪连接状态
不必建立连接或重启状态机。
- 不需要拥塞控制
不内置客户端或网络反馈机制。

### udp协议特点
1. UDP是无连接的，即发送数据之前不需要建立连接，因此减少了开销和发送数据之前的时延。
2. UDP使用尽最大努力交付，即不保证可靠交付，因此主机不需要维持复杂的连接状态表。
3.  UDP是面向报文的。发送方的UDP对应用程序交下来的报文，在添加首部后就向下交付IP层。**UDP对应用层交下来的报文，既不合并，也不拆分，而是保留这些报文的边界**。
4. UDP没有拥塞控制，因此网络出现的拥塞不会使源主机的发送速率降低
5. UDP支持一对一、一对多、多对一和多对多的交互通信。

### NAT穿透
TURN、STUN、ICE，用于在 UDP 主机之间建立端到端的连接。

STUN： STUN 服务器的 IP 地址已知（通过 DNS 查找或手工指定），应用程序首先向
STUN 服务器发送一个绑定请求。然后，STUN 服务器返回一个响应，其中包含在外
网中代表客户端的 IP 地址和端口号。
• 应用程序可以获得外网 IP 和端口，并利用这些信息与对端通信；
• 发送到 STUN 服务器的出站绑定请求将在通信要经过的 NAT 中建立路由条目，
使得到达该 IP 和端口的入站分组可以找到内网中的应用程序；
• STUN 协议定义了一个简单 keep-alive 探测机制，可以保证 NAT 路由条目不超时。

TURN: 这个协议依赖于外网中继设备（图 3-6）在
两端间传递数据。
• 两端都要向同一台 TURN 服务器发送分配请求来建立连接，然后再进行权限协商。
• 协商完毕，两端都把数据发送到 TURN 服务器，再由 TURN 服务器转发，从而
实现通信。

ICE: ICE 规定了一套方法，致力于在通信各端之间建立一
条最有效的通道（图 3-7）：能直连就直连，必要时 STUN 协商，再不行使用 TURN。