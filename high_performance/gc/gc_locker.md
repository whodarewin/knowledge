# gc locker 问题
## 简介
jni是解决java性能问题的一种方式，但jni在使用的过程中，会存在一些问题，其中向jni调用传递数组对象，便是其中之一，因为不是复制而是直接传递引用，所以在jni还在使用数组对象的时候，gc便无法回收这个对象，进而无法回收整个区域，对jni使用的对象的保护，便是使用的gc_locker，当数组传递进jni之前，会使用gc_locker先锁定这一个区域，等jni调用完毕，gc_locker再释放这个区域。
## 注意事项
如果传递给jni的数组长时间不能够解除gc_locker，则新生代不能被回收，垃圾回收器会选择在老年代分配临时对象，降低系统gc效率。
## 引用
[江南白衣-gc locker](http://calvin1978.blogcn.com/articles/jni.html)