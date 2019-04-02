#缓存推荐
## 传统的guava cache
    想必这个是大家最熟知的guava cache了，作为最古老的LRU cache，现在仍然在很多系统中运行，对其介绍如下。
    1. guava cache定义了cache创建的接口模式，并在后续新型cache中。
    2. guava cache借鉴ConcurrentHashMap做的存储和自定义的LRU链表。
    3. guava cache在高并发下存在严重的锁竞争问题（维护LRU链表的竞争）。
    性能已经是很差了，不建议使用。
## caffeine cache
    基于W-TinyLFU算法做的缓存，只能使用jdk1.8，性能上做了非常多的优化，比guava cache性能高很多，优化点还记得的有这么几个
    1. 基于W-TinyLFU，提升了缓存的命中率
    2. 针对W-TinyLFU记录更新频率的组件的更新操作，使用多个ring-buffer的结构作为缓冲，减少更新的锁竞争（提供这种优化的还有fork join pool）。
    3. 缓存的清除放在单一线程中清除，不会给查询线程和更新线程带来时间上的损耗。
    4. 使用1.8的ConcurrentHashMap做缓存组件，分段锁粒度更低（一个桶一个)，查询更快（链表变红黑树）
## cache2k
    最近看到的一个缓存，存在时间也不短了，还没研究，先贴上benchmark test，后续补充上。
[test](https://cruftex.net/2017/09/01/Java-Caching-Benchmarks-Part-3.html)