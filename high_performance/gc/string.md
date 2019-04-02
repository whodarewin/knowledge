# gc
## String优化的意义
    String对象在应用中占据的内存空间是排在前列的，大家可以用MAT等堆查看工具查看String对象在堆中的占比，没有意外应该是排在前面的，所以对String的优化意义重大。
## 如何优化
### StringBuilder优化
    频繁创建的需要链接生成的小长度String对象，将StringBuilder与每个线程绑定，创建完毕String后，StringBuilder重置，供下一次创建使用，减小内存消耗。
    举例说明：
    我们每次去redis里面查询数据，都需要手工拼接一个key，每次拼接key，创建StringBuilder耗费空间，这时使用Thread绑定的StringBuilder创建，节省内存。
    注：线程绑定StringBuilder可使用ThreadLocal。
### 
