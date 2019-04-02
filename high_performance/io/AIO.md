# IO
## AIO
    还不怎么太了解，没用过，基于以前从网上看到的事情，看了一下，以后更新。
### 介绍
    AIO 是对NIO的改进，所以又叫NIO.2，计划中的aio是要着重解决nio的一些问题的，但linux到现在还没有解决好。
### 实现
    AIO的实现和NIO的实现，差别在是谁将内核中的数据拷贝到用户控件，NIO来说，是用户线程自己拷贝，而对于AIO来说，是内核给我们准备好。
### 优点：
    将内存copy这份工作，换成内核线程来做，解放了用户线程。
### 缺点：
    windows 使用iocp实现aio，支持的比较好。
    linux 并不成熟，底层都是基于epoll，并没有看到很好的效率提升，这里借用netty作者干掉linux aio的链接说明问题。
[NIO.2 support · Issue #2515 · netty/netty · GitHub](https://github.com/netty/netty/issues/2515)    
### 工程映射
    netty实现了又废了（见上面）
    目前很小众（或者很多人用了我不知道？希望有人能够告诉我）
### 后续
    由于linxu对aio技术的不成熟，据笔者所知，aio在以linux为基础系统的互联网领域用的还比较少。