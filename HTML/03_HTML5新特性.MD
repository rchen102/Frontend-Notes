### 03_HTML5新特性
- 语义化标签
- 表单新控件，新的Input类型：date time email url search等；新的表单属性 placeholder required
- 新的元素，多媒体：用于媒介回放的 video 和 audio 元素；图像效果：用于绘画的 canvas 元素，svg元素
- 新的API，地理定位API：Geolocation；鼠标拖拽API：drag、drop
- 新的技术Webworker, WebSocket
- 离线 & 存储，对本地离线存储的更好的支持及Web Storage


#### 1 语义化
- **常见的语义化标签**：nav, aside, article, section, footer(以上为H5新出的), p, h
- **定义**：根据内容的结构化（内容语义化），选择合适的标签（代码语义化）便于开发者阅读和写出更优雅的代码的同时让浏览器的爬虫和机器很好地解析
- **特点**：视觉表现上差不多，主要区别在于它们表示了不同的语义
- **优点**：
	- 对开发者更友好：增加了代码的可读性，即便在没用CSS的时候，开发者也能清晰的看出网页的结构
	- 对机器也很友好，适宜机器阅读，如有利于SEO，让搜索引擎爬虫更好地获取更多地有效信息，此外还能支持读屏软件
- **个人看法**：用对比不用好，不用比用错好。HTML用于描述软件界面多过于富文本，这种情况下没必要
	- 自然语言表达能力的补充
	- 文章标题摘要
	- 适合机器阅读的整体结构

#### 2 Webworker
- **目的**：为 JavaScript 创造多线程环境，允许主线程创建 Worker 线程，将一些任务分配给后者运行。
- **好处**：一些计算密集型或高延迟的任务，被 Worker 线程负担了，主线程（通常负责 UI 交互）就会很流畅，不会被阻塞或拖慢。

>[注意事项](http://www.ruanyifeng.com/blog/2018/07/web-worker.html)：
> - **同源限制**： 分配给 Worker 线程运行的脚本文件，必须与主线程的脚本文件同源
> - **DOM限制**：Worker 线程所在的全局对象，与主线程不一样，无法读取主线程所在网页的 DOM 对象，也无法使用document、window、parent这些对象。但是，Worker 线程可以navigator对象和location对象
> - **通信联系**：Worker 线程和主线程不在同一个上下文环境，它们不能直接通信，必须通过消息完成
> - **脚本限制**：Worker 线程不能执行alert()方法和confirm()方法，但可以使用 XMLHttpRequest 对象发出 AJAX 请求
> - **文件限制**：Worker 线程无法读取本地文件，即不能打开本机的文件系统（file://），它所加载的脚本，必须来自网络

#### 3 WebSocket
- **定义**：[WebSocket](https://www.cnblogs.com/fuqiang88/p/5956363.html)是HTML5开始提供的一种在单个 TCP 连接上进行全双工通讯的协议
- **说明**：在WebSocket API中，浏览器和服务器只需要做一个握手的动作，然后，浏览器和服务器之间就形成了一条快速通道，两者之间就可以通过 TCP 连接直接交换数据。
- **使用**：获取 Web Socket 连接后，你可以通过 send() 方法来向服务器发送数据，并通过 onmessage 事件来接收服务器返回的数据
- **Why**：
	- HTTP 协议是一种无状态的、无连接的、单向的应用层协议。它采用了请求/响应模型。通信请求只能由客户端发起，服务端对请求做出应答处理。弊端：HTTP 协议无法实现服务器主动向客户端发起消息。
	- 如果服务器有连续的状态变化，客户端要获知就非常麻烦。大多数 Web 应用程序将通过频繁的异步JavaScript和XML（AJAX）请求实现长轮询。轮询的效率低，非常浪费资源

####  4 HTML5的文件离线储存（应用程序缓存）
- 浏览器发现`<html>`标签中包含 manifest 属性，它会请求manifest文件
- 如果是第一次访问，那么浏览器就会根据manifest文件的内容下载相应的资源，并进行离线存储
- 如果已经访问过并且资源已经离线存储了，那么浏览器就会使用离线的资源加载页面
- 然后浏览器会对比新的manifest文件与旧的manifest文件，如果文件没有发生改变，就不会做任何操作，如果文件改变了，那么就会重新下载文件中的资源，并且进行离线存储

#### 5 HTML5 Web Storage
- HTML5可以在本地存储用户的浏览数据,提供了两种在客户端存储数据的新方法：
	- localStorage - 没有时间限制的数据存储
	- sessionStorage - 针对一个 session 的数据存储, 当用户关闭浏览器窗口后，数据会被删除

#### 6 cookies，sessionStorage和localStorage的区别
- cookies是为了标识用户身份而存储在用户本地终端上的数据，始终在同源http请求中携带，即cookies在浏览器和服务器间来回传递，而sessionstorage和localstorage不会自动把数据发给服务器，仅在本地保存。
- 存储大小的限制不同。cookie保存的数据很小，不能超过4k，而sessionstorage和localstorage保存的数据大，可达到5M。
- 数据的有效期不同。cookie在设置的cookie过期时间之前一直有效，即使窗口或者浏览器关闭。sessionstorage仅在浏览器窗口关闭之前有效。localstorage始终有效，窗口和浏览器关闭也一直保存，用作长久数据保存
- 作用域不同。cookie在所有的同源窗口都是共享；sessionstorage不在不同的浏览器共享，即使同一页面；localstorage在所有同源窗口都是共享