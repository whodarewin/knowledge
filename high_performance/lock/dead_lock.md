# 死锁dead lock
## 介绍
    死锁是并发编程中经常遇到的问题，这个问题的成因是线程A持有资源1，需要获取资源2，但是线程B持有资源2，要获取资源1。
## 死锁的发现
    jstack 提供了死锁检测功能，像下面这样
    Deadlock Detection:
    
    Found one Java-level deadlock:
    =============================
    
    "Thread1":
      waiting to lock Monitor@0x0005c750 (Object@0xd4405938, a java/lang/String),
      which is held by "Thread2"
    "Thread2":
      waiting to lock Monitor@0x0005c6e8 (Object@0xd4405900, a java/lang/String),
      which is held by "Thread1"
    
    Found a total of 1 deadlock.
    但他是真正的检测锁，别的检测不了，而死锁宽泛的定义，其实是对资源的占用，有一些死锁不是因为真正的锁导致，而是由于资源竞争导致，如下：潜在死锁情况列举的第一种，这种就要肉身debug了。
## 潜在死锁情况列举
    有一些死锁情况，比较特殊，不会被jvm自动识别，需要人工肉体debug才能发现，现在列举一个。
    1. 有一个应用公用的线程池，线程A使用线程池执行一个任务，这个任务又使用了这个线程池执行另外一个任务，假设线程池队列数量为0，便形成了死锁，这个情况也可以扩大到多个线程的情况，即线程池套用，慎重使用。
    2. 记得还有一个web class load的死锁，忘记了，想起来再更。