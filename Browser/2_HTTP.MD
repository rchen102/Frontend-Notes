## 2_HTTP

HTTP协议是基于TCP协议的纯粹的文本协议

TCP协议是一条双向通道，HTTP在TCP的基础上，规定了Request-Response的模式（决定了通讯必定是浏览器先发起）

HTTP格式
- Request
	- request line (First line)
		- method
		- path
		- version （协议和版本）
	- head (请求头)
	- body (请求体)
- Response
	- response line (First line)
		- status code
		- status text
		- verison （协议和版本）
	- head (响应头)
	- body (响应体)

### 1 method
- Get：获取资源，通过URL提交数据，常用于向服务器查询信息
- Post: 传输实体文本，数据放置于HTTP报文的主体，表单提交产生该方法
- Put： 添加资源，在请求报文的主体中包含文件内容，然后保存在请求URI指定的位置
- Delete：删除资源，与Put相反
- Head：与Get一样，但是不返回报文的主体部分，用于确认URI的有效性及资源更新的日期时间
- Connect：多用于HTTPS和WebSocket
- Options：询问支持的方法（可以提交哪些请求方法），一般用于调试
- Trace：追踪路径，对请求消息的传输路径进行追踪，一般用于调试

### 2 status code & status text
common status code:
- 1xx: 临时响应，表示客户端请继续 （由浏览器http模块直接处理掉，不会让上层应用知晓）
- 2xx: 请求成功
	- 200: 请求成功
- 3xx: 表示请求的目标有变化，希望客户端进一步处理
	- 301&302: 永久性与临时性跳转
	- 304: 与客户端缓存没有更新 （客户端本地已有缓存版本，并在Request中告诉了服务端）
- 4xx: 客户端请求错误
	- 403: 无权限
	- 404: 表示请求的页面不存在
	- 418: teapot, 彩蛋
- 5xx: 服务端请求错误
	- 500: 服务端错误
	- 503: 服务端暂时性错误，可以稍后再试

### 3 head
HTTP头可应看作一个键值对，原则上HTTP头是一种数据，可以自定义键和值

| Request Header     |     规定  |
| :-------- | :--------| 
| Accept   |   浏览器端接受的格式 |
| Accept-Encoding   |   浏览器端接受的编码方式 |
| Accept-Language   |   浏览器端接受的语言，用于服务端判断多语言 |
| Cache-Control  |   控制缓存的时效性 |
| Connection |   连接方式，若是keep-alive，且服务端支持，则会复用连接 |
| Host  |   HTTP访问使用的域名 |
| Cache-Control  |   控制缓存的时效性 |
| If-Modified-Since  |   上次访问时的更改时间，若服务器认为此时间后自己未更新，返回304 |
| If-None-Match  |   此访问时使用的ETag，通常是页面信息摘要，比更改时间更准确 |
| User-Agent  |   客户端标识 |
| Cookie  |   客户端存储的cookie字符串 |

| Response Header     |     规定  |
| :-------- | :--------| 
| Cache-Control   |   缓存控制，用于通知各级缓存保存时间 |
| Connection |   连接方式，keep-alive表示复用连接 |
| Content-Encoding  |   内容编码格式，通常是gzip |
| Content-Length  |   内容的长度，有利于浏览器判断内容是否已经结束 |
| Content-Type  |   内容类型，所有请求网页的都是text/html |
| Date  |   当前的服务器日期 |
| ETag  |  页面的信息摘要，用于判断是否重新需要到服务器端取页面 |
| Expires  |  过期时间，用于判断下次请求是否重新需要到服务器端取页面 |
| Keep-Alive |  保持连接不断时需要的一些信息，如timeout=5, max=100 |
| Last-Modified  |   页面上次修改时间  |
| Server  |  服务器端的软件类型 |
| Set-Cookie |   设置cookie，可以存在多个 |
| Via  |   服务端的请求链路，对一些调试场景至关重要 |

### 4 body
请求的body主要用于表单提交场景，也可自定义使用
Request body type: 
- application/json
- application/x-www-form-urlencoded （html form标签提交）
- multipart/form-data （文件上传）
- text/html

### 5 其他
#### HTTPS：
HTTPS使用加密通道来传输HTTP的内容，HTTPS首先与服务端建立一条TLS加密通道，TLS构建于TCP协议之上，它实际上是对传输内容做一次加密，从传输内容方面看，HTTPS于HTTP并无区别

- 以HTTP协议为基础，保持HTTP的设计思想，即Request-Response模式
- 作用：
	- 确定请求的目标服务端身份
	- 保证传输的数据不会被网络中间节点窃听或篡改

#### HTTP2:

- 以HTTP协议为基础，保持HTTP的设计思想，即Request-Response模式
- 特点：
	- 支持服务端推送，在客户端发送第一个请求到达时，提前推送一般部分内容至客户端缓存中，避免客户端请求顺序带来的并行度不高，从而导致的性能问题
	- 支持TCP连接复用：使用同一个TCP连接来传输多个HTTP请求，避免了TCP连接建立时三次握手的开销和初建TCP连接时传输窗口小的问题

