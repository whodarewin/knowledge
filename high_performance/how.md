# 如何进行性能优化
我们在遇到应用应能问题后，应该以何种思路进行性能优化？大方向是什么？  
工作中常见的方法有
1. 链路法：从请求开始到请求接受到结果整个链路，按照请求链路进行性能分析，看到耗费性能最大的点，重点进行优化。
2. 随机法：拍脑袋决定的优化方法，感觉这个地方性能不好，便对这个地方进行优化，但感觉是种奇妙的东西。    

显而易见的，第二种是错误的。
我们使用链路法进行分析，可进行性能优化的点为
1. 序列化：序列化协议优化：json-hession等
2. 传输协议层面：HTTP1.0 1.1 2.0 quic协议
3. IO：bio-nio-aio
4. jvm层面：这个太多了，看后面章节
5. 数据库层面：传统行列式数据库-kvdb。。。
6. 架构层面：缓存，分布式计算等。。。