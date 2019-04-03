# 知识体系 #
# 基点 #
``` 一切技术的存在都是为了解决问题，如果一项技术没有解决问题的现实意义，技术便不存在意义 ```

## 软件评价体系 ##
```如何量化你的软件```
- [QPS,SLA...](https://github.com/whodarewin/knowledge_hierarchy/blob/master/evaluation/evaluation.md)
- [其余代码检测工具](https://github.com/whodarewin/knowledge_hierarchy/blob/master/evaluation/tool.md)


## 高性能 ##

- IO
```如何使用最少的资源，从IO设备搬运最多的字节```
    - [物理层的演进](https://github.com/whodarewin/knowledge_hierarchy/blob/master/high_performance/io/)
    - [协议层的演进](https://github.com/whodarewin/knowledge_hierarchy/blob/master/high_performance/io/)
        - TCP/IP协议及其演进
        - HTTP及其演进
    - [应用层的演进](https://github.com/whodarewin/knowledge_hierarchy/blob/master/high_performance/io/)
	    - [BIO](https://github.com/whodarewin/knowledge_hierarchy/blob/master/high_performance/io/BIO.md)
	    - [NIO](https://github.com/whodarewin/knowledge_hierarchy/blob/master/high_performance/io/NIO.md)
	    - [AIO](https://github.com/whodarewin/knowledge_hierarchy/blob/master/high_performance/io/AIO.md)
	    - [IO设计模式](http://github.com/whodarewin/knowledge_hierarchy/blob/master/high_performance/io/design.md)
	    - 零拷贝
	    - 顺序读写
	    - 缓存
	        - [缓存推荐](https://github.com/whodarewin/knowledge_hierarchy/blob/master/high_performance/other/cache_recommend.md)-
- CPU
```如何让CPU更快的运算你的逻辑```
    - CPU的演进
        - 乱序执行
        - 可见性
        - 缓存行
	- CODER的奋斗
	    - 缓冲行填充
        - 并发：
	    - 锁竞争
		    - 传统悲观锁
		    - cas锁机制
		    - [死锁](https://github.com/whodarewin/knowledge_hierarchy/blob/master/high_performance/lock/dead_lock.md)
		    - 线程数计算
        - GC
	        - 垃圾回收器
	        - [String对象处理](https://github.com/whodarewin/knowledge_hierarchy/blob/master/high_performance/gc/string.md)
	        - [缓存问题](https://github.com/whodarewin/knowledge_hierarchy/blob/master/high_performance/gc/cache.md)
	        - GC优化的原则
- 其他：

## 分布式 ##
```如何解决单机无法解决的问题```
    - 有状态与无状态
    - 副本机制
    - 一致性
	    - CAP
	    - BASE理论
	    - PAXOS
	    - RAFT
	    - 基于队列
	    - 负载均衡
    - 降级熔断限流


## 数据库 ##
```如何解决数据快速落地与个性化查询的问题```
- 模型
	- BTree
	- LSM树
	- 基于内存的数据库

## 算法 ##
```如何更快的执行你的业务逻辑+锻炼你的程序员大脑```
- array&链表
- 哈希表
- 红黑树
- 跳表


## [代码设计](https://github.com/whodarewin/knowledge_hierarchy/blob/master/code/design.md)
```如何解决代码后续可读性，维护性问题```

## 团队合作
```如何在技术上激发各个团队人员的积极性，降低沟通成本```
## 常用工程架构
- rpc系统
- 队列系统
- 分布式调度系统
- 分布式配置系统


## [关于技术的落地](https://github.com/whodarewin/knowledge_hierarchy/blob/master/achievement/achievement.md)
