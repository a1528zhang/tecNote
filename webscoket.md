## WebSocket

---

WebSocket 是一个全新的、独立的协议，基于 TCP 协议，与 HTTP 协议兼容却不会融入 HTTP 协议，仅仅作为 HTML5 的一部分。它是一种与 HTTP 同等的网络协议，两者都是应用层协议，都基于 TCP 协议。但是 WebSocket 是一种双向通信协议，在建立连接之后，WebSocket 的 server 与 client 都能主动向对方发送或接收数据。同时，WebSocket 在建立连接时需要借助 HTTP 协议，连接建立好了之后 client 与 server 之间的双向通信就与 HTTP 无关了。

![通信过程](https://pic2.zhimg.com/80/v2-361334a3f98fb379672d837d894c19fb_hd.jpg)

如图，首先由客户端先发起http请求通知server这是一个ws请求，server收到后返回消息，之后协议切换为ws，然后client与server可以互相通信，其中有任意一方结束连接ws就关闭。

client的http请求报文头中包含：
- "Upgrade: websocket"： 表明这是一个 WebSocket 类型请求，意在告诉 server 需要将通信协议切换到 WebSocket

- "Sec-WebSocket-Key: *": 是 client 发送的一个 base64 编码的密文，要求 server 必须返回一个对应加密的 "Sec-WebSocket-Accept" 应答，否则 client 会抛出 "Error during WebSocket handshake" 错误，并关闭连接

server收到http请求后的应答报文：
- "HTTP/1.1 101 WebSocket Protocol Handshake"：返回的状态码为 101，表示同意 client 的协议转换请求

- "Upgrade: websocket"

- "Connection: Upgrade"

- "Sec-WebSocket-Accept: *"