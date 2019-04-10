# 物理层的演进
## 评价指标
    IOPS：每秒的读写次数。
    Throughput:每秒钟传输的数据量。
## 硬盘物理层的演进
    传统的磁盘本质上是一种物理装置，他的指标项有
    转速：通常为5400/7200/10K/15K 不等
    寻道时间：是指将读写磁头移动至正确的磁道上所需要的时间。寻道时间越短，I/O操作越快，目前磁盘的平均寻道时间一般在3－15ms。
    旋转延迟：是指盘片旋转将请求数据所在扇区移至读写磁头下方所需要的时间。旋转延迟取决于磁盘转速，通常使用磁盘旋转一周所需时间的1/2表示。比如，7200转的磁盘平均旋转延迟大约为60*1000/7200/2 = 4.17ms，而转速为15000磁盘其平均旋转延迟约为2ms。
    数据传输时间：是指完成传输所请求的数据所需要的时间，它取决于数据传输率，其值等于数据大小除以数据传输率。目前IDE/ATA能达到133MB/s，SATA II可达到300MB/s的接口数据传输率，数据传输时间通常远小于前两部分时间。
    其IOPS计算公式为 IOPS = 1000 ms/ (寻道时间+旋转延迟+数据传输时间)。
    这里有从网上找到的两组数据
    5400转笔记本硬盘平均读写速度大致在60-90MB这个区间
    7200转台式机硬盘大致在130-190MB区间，10000转的西数黑盘也在这个区间内
    我们说磁盘IO慢，就慢在了磁盘机械效率上。
    
    因此，新一代的SSD硬盘出现了，
    固态硬盘减少了磁盘的寻道时间+旋转延迟，只剩下数据传输时间，大大提高了传输效率。
    以下是一组数据
    固态硬盘读写速度与容量成正比，目前市售的至少300MB+
    1TB固态硬盘普遍500MB+
    2013新Mac Pro采用PCIE连接方式的SSD可以达到700MB左右
## 伴随着SSD硬盘而发展的工程
    SSD硬盘的高数据传输效率，带起了一批新的应用层技术。
    1. 基于磁盘的高效KV读写
        ROCKSDB，MAPDB等KV数据库
    2. 基于磁盘的二级缓存
        HBASE实现了外接SSD磁盘的高效二级缓存，用于提升直接从HDFS上读取数据的效率。
    。。。。
## 网络传输
    1. 2G到5G无线网络的演进
    现在我们还在4G的时代，3-4G导致了移动端互联网的发展，伴随着4G，落地了一大批技术
    及商业形态，现在5G已经开始试用，5G主要是解决了大数据量传输+万物互联的问题。
    伴随着5G的兴起，最终还会有一批技术落地，以解决我们需求中现有的问题，期待。。。
    搭一波5G的东风，我40岁应该还是可以开心的打代码吧。。。。
    2. 硬中断到DMA到带有DMA收集功能的DMA
    这个属于网卡的演进，原始的网卡数据的接受需要发送一个硬中断给CPU，CPU会响应这个
    中断，停止手中的活，将网卡中的数据读取到内核缓冲区，在网络大流量情况下，会出现
    CPU忙于响应中断而拖慢系统的情况。
    为了解决这个问题，DMA技术产生，DMA会将网卡数据直接拷贝到内核缓冲区，不用cpu做
    任何工作，从而解放了cpu。
    但如果我想把硬盘上的设备写入网络，那还是需要两次数据拷贝，或者直接使用transferTo，
    不拷贝入用户空间，直接从内核空间拷贝，由硬盘的内核空间到socket的内核空间，还是需
    要一次，那怎么办呢？带有收集功能的DMA解决了这个问题，将数据的地址和长度直接发送给
    DMA，DMA便会去读取数据发送。
    3. 网卡多队列
    如果DMA只有一个队列（缓冲区），那么就只能发送一个中断，让cpu中的一个核来处理，那
    么如果有多个呢？就可以多唤醒几个核来处理了，这就是网卡多队列，但是注意，网卡支持
    多队列，必须要操作系统也支持才可以！！！