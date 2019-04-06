## 介绍 ##
&emsp;&emsp; 零复制（英语：Zero-copy；也译零拷贝）技术是指计算机执行操作时，CPU不需要先将数据从某处内存复制到另一个特定区域。这种技术通常用于通过网络传输文件时节省CPU周期和内存带宽。  
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;-摘录自维基百科
## 实现 ##
&emsp;&emsp;带有dma 收集功能的零拷贝实现，计算机通过DMA将数据拷贝到内核缓冲区，然后cpu将内存地址发送给dma，然后直接再通过DMA将数据拷贝到外部设备，期间，cpu不执行任何的内存拷贝操作，全部通过DMA处理。  
&emsp;&emsp;不带有dma收集功能的零拷贝实现，  
&emsp;&emsp;mmap零拷贝实现  
## 优点 ##
可以更快速的实现外设数据转移的速度，可以高效的完成数据磁盘到socket，socket到socket，socket到磁盘的传输，通常用于网络传输时节省cpu和内存带宽。
## 工程映射 ##
kafka在接受消息并转发的时候，使用零拷贝技术提升传输效率。
java中的映射：
