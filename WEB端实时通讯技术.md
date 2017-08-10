# WEB端实时通讯的四种方式

浏览器本身作为一个瘦客户端，不具备直接通过系统调用来达到和处于异地的另外一个客户端浏览器通信的功能。这和我们桌面应用的工作方式是不同的，通常桌面应用通过socket可以和远程主机上另外一端的一个进程建立TCP连接，从而达到全双工的即时通信。

浏览器从诞生开始一直走的是客户端请求服务器，服务器返回结果的模式，即使发展至今仍然没有任何改变。所以可以肯定的是，要想实现两个客户端的通信，必然要通过服务器进行信息的转发。例如A要和B通信，则应该是A先把信息发送给IM应用服务器，服务器根据A信息中携带的接收者将它再转发给B，同样B到A也是这种模式。

## 1.Ajax短轮询
Ajax无法满足实时通信富交互式应用的实时更新数据的要求，因为它是基于HTTP协议的，HTTP协议请求和响应的模式是无法改变的，所以就注定Ajax无法满足要求。

## 2.Comet

实现Comet有两种方式：**长轮询**和**HTTP流**。

### 长轮询    
> 短轮询是定时向服务器发送请求，看有没有更新的数据，服务器收到请求后立马返回数据，不管有没有> 更新。 
>  
> 而长轮询是页面发起一个请求，然后服务器一直保持连接打开，直到有数据发送。
### HTTP流
浏览器向服务器发送一个请求，而服务器保持连接打开，然后周期性地向浏览器发送数据。
## 3.SSE
SSE（Server-Sent Event，服务端推送事件）是一种允许服务端向客户端推送新数据的HTML5技术。与由客户端每隔几秒从服务端轮询拉取新数据相比，这是一种更优的解决方案。
## 4.WebSocket
### WebSocket的目标
WebSocket是HTML5开始提供的一种在单个 TCP 连接上进行全双工通讯的协议。
在WebSocket API中，浏览器和服务器只需要做一个握手的动作，然后，浏览器和服务器之间就形成了一条快速通道。两者之间就直接可以数据互相传送。

在一个单独持久连接上提供全双工、双向通信。
### 步骤
1.实例一个WebSocket对象并传入要连接的URL，客户端和服务器就会尝试连接。
    
    var socket = new WebSocket("ws://www.example.com/server.php");
注意：传入的url必须是绝对url。   
2.一个HTTP请求会发送到浏览器，在取得服务器的响应后，建立的连接会使用HTTP升级从HTTP协议交换为WebSocket协议；
3.WebSocket打开之后，就可以通过send()方法传入任意的字符串：
    
    var socket = new WebSocket("ws://www.example.com/server.php");
    socket.send("Hello World!");
4.服务器要读取其中的数据，就是要解析接收到的JSON字符串。
5.服务器向客户端发来消息时，WebSocket会触发message事件。这个message事件会把返回的数据保存在event.data属性中：

    socket.onmessage = function(){
    	var data = event.data;
    	//处理数据
    };

### WebSocket缺点

对浏览器的兼容性，IE9+。


参考文献：  
[1] 《JavaScript高级程序设计》  
[2] [http://www.52im.net/thread-336-1-1.html](http://www.52im.net/thread-336-1-1.html)    
[3] [http://www.cnblogs.com/linsanshu/p/5759174.html](http://www.cnblogs.com/linsanshu/p/5759174.html)  
[4] [http://www.cnblogs.com/imstudy/p/5696033.html](http://www.cnblogs.com/imstudy/p/5696033.html)
