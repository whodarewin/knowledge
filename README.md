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
    - [物理层的演进](https://github.com/whodarewin/knowledge_hierarchy/blob/master/high_performance/io/physical_layer.md)
    - 协议层的演进
        - [HTTP及其演进]()
    - [应用层的演进](https://github.com/whodarewin/knowledge_hierarchy/blob/master/high_performance/io/)
	    - [BIO](https://github.com/whodarewin/knowledge_hierarchy/blob/master/high_performance/io/BIO.md)
	    - [NIO](https://github.com/whodarewin/knowledge_hierarchy/blob/master/high_performance/io/NIO.md)
	    - [AIO](https://github.com/whodarewin/knowledge_hierarchy/blob/master/high_performance/io/AIO.md)
	    - [IO设计模式](http://github.com/whodarewin/knowledge_hierarchy/blob/master/high_performance/io/design.md)
	    - [零拷贝](http://github.com/whodarewin/knowledge_hierarchy/blob/master/high_performance/io/zero-copy.md)
	    - [顺序读写](http://github.com/whodarewin/knowledge_hierarchy/blob/master/high_performance/io/SEQ.md)
	    - 缓存
	        - 缓存分层
	        - 缓存一致性问题
	        - [缓存推荐](https://github.com/whodarewin/knowledge_hierarchy/blob/master/high_performance/other/cache_recommend.md)

- CPU
```如何让CPU更快的运算你的逻辑```
    - CPU的演进
        - 乱序执行
        - 可见性
        - 缓存行
        - 超线程
	- CODER的奋斗
	    - 缓冲行填充
        - 并发：
	    - 锁竞争
		    - 传统悲观锁
		    - cas锁机制
		    - [死锁](https://github.com/whodarewin/knowledge_hierarchy/blob/master/high_performance/lock/dead_lock.md)
	    - 线程数计算
	    - 异步编程之于IO
	        - 介绍
	        - 基于队列的快速回调
- java 优化
    - java 性能分析
        - 锁竞争
        - 方法执行时长
    - GC
        - GC优化的原则
    	    - 垃圾回收器
    	    - [String对象处理](https://github.com/whodarewin/knowledge_hierarchy/blob/master/high_performance/gc/string.md)
    	    - [byte[] 复用]()
    	    - [缓存问题](https://github.com/whodarewin/knowledge_hierarchy/blob/master/high_performance/gc/cache.md)
    	    - 堆外内存及其回收
    	    - gc分析
- linux 
    - 容器化技术
        - cgroup
        - docker
        - vmware
        	        
- 其他：
    - java 高性能的那点事
        - [wait notify的不足与LockSupport的应用](https://issues.apache.org/jira/browse/HBASE-21628)
        - [误用LinkedTransferQueue导致的OOM](https://github.com/whodarewin/knowledge_hierarchy/blob/master/high_performance/other/LinkedTransferQueue_OOM.md)
    - [高性能存在的窘态](https://github.com/whodarewin/knowledge_hierarchy/blob/master/high_performance/other/embarrassed.md)
    - 进行性能分析的工具
    
## 高可用 ##
- 分布式
```如何解决单机无法解决的问题（稳定性，高计算量）```
    - 基础
        - [数据传输](https://github.com/whodarewin/knowledge_hierarchy/blob/master/high_availability/gc/transfer.md)
        - 负载均衡
        - 有状态与无状态
    - 分布式计算
        - 无状态计算
        - MR
        - 流式计算
    - 分布式存储
        - 副本机制
            - 一致性
                - CAP
                - BASE理论
                - PAXOS
            	- RAFT
            	- 基于队列
            	- 幂等
- 自我保护
```你的系统在非正常状态下的正常运行的能力（正常状态下没几个出问题的，除非bug）```
    - [AWS的Design for failure](https://www.slideshare.net/AmazonWebServices/best-practices-for-architecting-in-the-cloud-jeff-barr/20-5_Think_Parallel_Serial_and)
    - 峰值流量处理
        - 降级
        - 熔断
        - 限流
        - 写入缓冲
        - 平滑扩容
    - 网络故障
        - 异地多活
- 异常情况快速处理
    - 监控与报警与日志（重要重要重要，不重视监控系统的公司，一定是对技术有误解的公司）
    

## 数据库 ##
```如何解决数据快速落地与个性化查询的问题```
- 传统关系型数据库
    - BTree
- KV数据库
	- LSM树
	- 基于内存的数据库
	    - redis
- 时序数据库
    - opentsdb
    - druid
    - influxdb

## 算法 ##
```如何更快的执行你的业务逻辑+锻炼你的程序员大脑```
- 工程用的多的
    - array&链表
    - 哈希表
    - 红黑树
    - 跳表
    - 布隆过滤器
    - 杨氏矩阵
    - bitmap
    - 时间轮
- 其余的

# 大数据 #
- 空白

## [代码设计](https://github.com/whodarewin/knowledge_hierarchy/blob/master/code/design.md)
```如何解决代码后续可读性，维护性问题```
- 基于领域模型的代码设计
- 性能与设计的权衡
- 代码设计的窘态

## 团队合作
```如何在技术上激发各个团队人员的积极性，降低沟通成本```
- 工作流程
    - git工作流
- 服务拆分
    - 单体架构
    - SOA
    - 微服务
    - 烟筒架构与中台架构
    

# 流程 #
- 故障处理流程
- 需求流程
- 流量增加

## 程序员的日常
```方法论与屁事碎碎念```
- [心态的稳定](https://github.com/whodarewin/knowledge_hierarchy/blob/master/daily/mentality.md)
- 目标与杂事
- 故障驱动型优化
- 假头脑风暴
- 一个有经验的程序员真的顶好几个无经验的程序员吗？
- 形式主义与实用主义
- 架构师为何喜欢看别人的分享：使用别人的经验降低自己的试错成本及必须要注意的问题
- 关于中国制造2025级程序员35岁后发展前途的问题
- 创新，创新的作用，去哪里做创新。
- 程序员写博客：觉得自己什么都懂，写起来发现什么都不懂
- 关于放权：你给我任务，我给你结果，但你却连监控要怎么加都指导一下，又因为具体了解的少，无法落地

## [关于技术的落地](https://github.com/whodarewin/knowledge_hierarchy/blob/master/achievement/achievement.md)

## 工具 ##
- JRE,JVM
- SPRING
- 分布式协调
    - zookeeper
    - etcd
- 网络通讯
    - netty
    - http-client

## 常用工程架构
- rpc系统
- 队列系统
- 分布式调度系统
- 分布式配置系统

## 后续计划看的
[弹力设计-希望能重新穿一遍分布式系统](http://www.360doc.com/content/18/0305/08/53055196_734370489.shtml)
