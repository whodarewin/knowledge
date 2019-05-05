# jedis 连接失效导致的gc 问题
## 背景
&emsp;&emsp;最近一个逻辑超级简单的应用，就是从redis里面取数据传回去，gc频率非常高，但访问量却不大。
## 分析过程
&emsp;&emsp;用mat分析dump下来的内存，发现byte[]和char[]数组特别多，联想到这个应用订阅了一个redis的pubsub消息，怀疑是