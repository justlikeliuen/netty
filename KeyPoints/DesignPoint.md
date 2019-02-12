#事件驱动
* ChannelHandler
* ChannelEvent

除了NIO的相关知识，另一个就是事件驱动的设计思想。
什么叫事件驱动？我们回头看看EchoServerHandler的代码，其中的参数：
public void messageReceived(ChannelHandlerContext ctx, MessageEvent e)，MessageEvent就是一个事件。
这个事件携带了一些信息，例如这里e.getMessage()就是消息的内容，而EchoServerHandler则描述了处理这种事件的方式。
一旦某个事件触发，相应的Handler则会被调用，并进行处理。这种事件机制在UI编程里广泛应用，而Netty则将其应用到了网络编程领域。

在Netty里，所有事件都来自ChannelEvent接口，这些事件涵盖监听端口、建立连接、读写数据等网络通讯的各个阶段。
而事件的处理者就是ChannelHandler，这样，不但是业务逻辑，连网络通讯流程中底层的处理，都可以通过实现ChannelHandler来完成了。
事实上，Netty内部的连接处理、协议编解码、超时等机制，都是通过handler完成的。
下图描述了Netty进行事件处理的流程。Channel是连接的通道，是ChannelEvent的产生者，而ChannelPipeline可以理解为ChannelHandler的集合。

# ZERO-COPY