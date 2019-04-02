# 设计模式
## 介绍
    围绕NIO和AIO，有两套设计模式相对应。
    1. reactor，对应NIO设计模式。
    2. proactor，对应AIO设计模式。
## 延伸的概念
    阻塞与非阻塞
    这个是和io相关的，
    1. 阻塞调用，在数据没有回来之前，线程一直等待。
    2. 非阻塞调用，在数据没有回来之前，线程可以去做别的事情。
    异步与同步
    1. 这个是和方法调用相关的
    2. 异步是说这个方法被调用后，可以直接返回，数据可以给callback处理，即只是通知一下。
    同步是说这个方法被调用后，必须要等到方法执行完毕，才能返回。
    主要是针对对象不一样。
## reactor 设计模式
![image text](https://github.com/whodarewin/knowledge_hierarchy/blob/master/high_performance/io/reactor.png)

    上图是对reactor模式的类图。
    EventHandler抽象类表示IO事件处理器，它拥有IO文件句柄Handle（通过get_handle获取），以及对Handle的操作handle_event（读/写等）。继承于EventHandler的子类可以对事件处理器的行为进行定制。Reactor类用于管理EventHandler（注册、删除等），并使用handle_events实现事件循环，不断调用同步事件多路分离器（一般是内核）的多路分离函数select，只要某个文件句柄被激活（可读/写等），select就返回（阻塞），handle_events就会调用与文件句柄关联的事件处理器的handle_event进行相关操作。

    下面是流程图。
![image text](https://github.com/whodarewin/knowledge_hierarchy/blob/master/high_performance/io/proactor_flow.png)

    下面是大部分基于NIO的线程分配模型。
![image text](https://github.com/whodarewin/knowledge_hierarchy/blob/master/high_performance/io/reactor_multi.png)

## proactor 设计模式

![image text](https://github.com/whodarewin/knowledge_hierarchy/blob/master/high_performance/io/proactor.png)
    
    上图是proactor模式的类图
    Proactor模式和Reactor模式在结构上比较相似，不过在用户（Client）使用方式上差别较大。Reactor模式中，用户线程通过向Reactor对象注册感兴趣的事件监听，然后事件触发时调用事件处理函数。而Proactor模式中，用户线程将AsynchronousOperation（读/写等）、Proactor以及操作完成时的CompletionHandler注册到AsynchronousOperationProcessor。AsynchronousOperationProcessor使用Facade模式提供了一组异步操作API（读/写等）供用户使用，当用户线程调用异步API后，便继续执行自己的任务。AsynchronousOperationProcessor 会开启独立的内核线程执行异步操作，实现真正的异步。当异步IO操作完成时，AsynchronousOperationProcessor将用户线程与AsynchronousOperation一起注册的Proactor和CompletionHandler取出，然后将CompletionHandler与IO操作的结果数据一起转发给Proactor，Proactor负责回调每一个异步操作的事件完成处理函数handle_event。虽然Proactor模式中每个异步操作都可以绑定一个Proactor对象，但是一般在操作系统中，Proactor被实现为Singleton模式，以便于集中化分发操作完成事件。
    
    下图为流程图
![image text](https://github.com/whodarewin/knowledge_hierarchy/blob/master/high_performance/io/proactor_flow.png)