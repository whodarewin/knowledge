# docker cpu降频导致的gc问题
## 现象
    2019-04-28T17:07:15.463+0800: 1125949.941: [GC (Allocation Failure) 2019-04-28T17:07:15.463+0800: 1125949.941: [ParNew: 498519K->87022K(546112K), 0.5020725 secs] 1060397K->655977K(1911488K), 0.5024580 secs] [Times: user=0.25 sys=0.00, real=0.50 secs]
## 排查    
&emsp;一般user+sys的时间是大于real的，因为在年轻代ParNew gc 并行收集，user和sys是多个线程共同的耗时，而real是stw的时间，user和sys加起来应该比real大才对，但这里是小的，只能是cpu在执行gc的过程中，申请不到一些资源，导致的，进一步观察docker 物理机器的 through time，发现在这个时间点有cpu针对此docker降频存在，故是在gc过程中，由于申请不到cpu资源，导致real时间增长导致。