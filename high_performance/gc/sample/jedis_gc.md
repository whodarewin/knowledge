# jedis 连接失效导致的gc 问题
## 背景
&emsp;&emsp;最近一个逻辑超级简单的应用，就是从redis里面取数据传回去，gc频率非常高，但访问量却不大。
## 分析过程
&emsp;&emsp;用mat分析dump下来的内存，发现byte[]和char[]数组特别多，如下图所示：

![mat 分析](https://github.com/whodarewin/knowledge_hierarchy/blob/master/high_performance/gc/sample/jedis_mat.png)

&emsp;&emsp;进一步分析，byte[]数组来自于Jedis的RedisOutputClient和RedisInputClient的buf，一个8kb。

![byte source](https://github.com/whodarewin/knowledge_hierarchy/blob/master/high_performance/gc/sample/jedis_byte.png)

&emsp;&emsp;char[]数组来自于JedisPool使用的GenericObjectPool的creationStackTrace。

![char source](https://github.com/whodarewin/knowledge_hierarchy/blob/master/high_performance/gc/sample/jedis_char.png)

&emsp;&emsp;再看等待被回收的对象，Jedis，和Jedis关联的RedisInputStream，RedisOutputStream有32147个等待被回收。

![jedis](https://github.com/whodarewin/knowledge_hierarchy/blob/master/high_performance/gc/sample/jedis_tobecollected.png)

&emsp;&emsp;考虑到有这么多的jedis连接等待被回收，有可能是jedis pool出了问题，经查询，JedisPool的配置为最大容纳100个，最多idle 30个，即产生的连接很容易被杀掉，造成内存gc问题，并且这个jedis集群的分片非常多，有一千多个，进一步佐证了这个想法。



