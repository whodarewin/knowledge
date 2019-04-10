# 起因 #
线上有一个服务，需要使用线程池去redis里面查询数据，需要使用容量为零的队列，java容量为零的队列有两个，LinkedTransferQueue
和SynchronizedQueue,上线时就直接使用了LinkedTransferQueue，不料应用直接OOM（幸亏是灰度发的十台）
# 分析 #
修改的代码就这一个，流程上也只有这一个是新增，所以问题锁定在了LinkedTransferQueue和线程池上面，看线程池源码，发现调用的是
offer方法，看LinkedTransferQueue的实现。  

        public boolean offer(E e, long timeout, TimeUnit unit) {
            xfer(e, true, ASYNC, 0);
            return true;
        }
永远return true;看注释，  

         * Inserts the specified element at the tail of this queue.
         * As the queue is unbounded, this method will never block or
         * return {@code false}.
         *
         * @return {@code true} (as specified by
         *  {@link BlockingQueue#offer(Object,long,TimeUnit) BlockingQueue.offer})
         * @throws NullPointerException if the specified element is null
         
unbounded！！！！！！！！

# 原因 #

突然想起来，LinkedTransferQueue是使用TransferQueue的接口方法实现零队列的，和ThreadPoolExecutor根本不兼容！！！如果你
调用offer的话，只能是一个无界队列！！！


