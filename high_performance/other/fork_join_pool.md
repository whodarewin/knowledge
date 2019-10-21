# ForkJoinPool
## 解决的是什么问题
就一个，递归任务多线程编程便利。
## 如何解决的
从jdk注解里面找到的
### RecursiveTask 
有返回值的
```java
class Fibonacci extends RecursiveTask<Integer> { 
    final int n;
    Fibonacci(int n) { this.n = n; }
    Integer compute() {
      if (n <= 1)
        return n;
      Fibonacci f1 = new Fibonacci(n - 1);
      f1.fork();
      Fibonacci f2 = new Fibonacci(n - 2);
      return f2.compute() + f1.join();
    }
}
```
### 无返回值的
RecursiveAction
```java
static class SortTask extends RecursiveAction {
    final long[] array; final int lo, hi;
    SortTask(long[] array, int lo, int hi) {
      this.array = array; this.lo = lo; this.hi = hi;
    }
    SortTask(long[] array) { this(array, 0, array.length); }
    protected void compute() {
      if (hi - lo < THRESHOLD)
        sortSequentially(lo, hi);
      else {
        int mid = (lo + hi) >>> 1;
        invokeAll(new SortTask(array, lo, mid),
                  new SortTask(array, mid, hi));
        merge(lo, mid, hi);
      }
    }
    // implementation details follow:
    static final int THRESHOLD = 1000;
    void sortSequentially(int lo, int hi) {
      Arrays.sort(array, lo, hi);
    }
    void merge(int lo, int mid, int hi) {
      long[] buf = Arrays.copyOfRange(array, lo, mid);
      for (int i = 0, j = lo, k = mid; i < buf.length; j++)
        array[j] = (k == hi || buf[i] < array[k]) ?
          buf[i++] : array[k++];
    }
  }
```
## 坑
### 全部线程被block的坑
如果你使用一个有返回值的，即RecursiveTask，然后写成下面这样
```java
class Fibonacci extends RecursiveTask<Integer> { 
    final int n;
    Fibonacci(int n) { this.n = n; }
    Integer compute() {
      if (n <= 1)
        return n;
      Fibonacci f1 = new Fibonacci(n - 1);
      f1.fork();
      Fibonacci f2 = new Fibonacci(n - 2);
      f2.fork();
      return f2.join() + f1.join();
    }
}
```
整个线程池会block，因为本身执行这个任务的线程全部没有执行任何计算任务，全部给block了，而本线程执行compute操作，所有的线程都在执行计算操作，不会产生这样的问题。
### 相比普通线程池的优化
### 对递归多线程任务的友好
加一个限制，大于等于两个分支的那种，一个分支的，单线程更快（没有了任务创建耗时，线程上下文切换耗时）
#### 多队列
减少队列头部锁竞争的耗时。
#### 窃取算法
多队列引起了线程饥饿的情况，即一个线程早早运行完毕了自身队列内的任务，而其余的线程却还在忙着自己的任务。便造成了线程饥饿的情况。  
ForkJoinPool解决了这部分的问题，采用的是工作窃取算法，闲置线程会找到其余线程的队列，这两个线程会从队列两端到中间消费消息。在一定程度上减少了线程饥饿情况的出现，当然也不能完全避免，因为最多一个队列只能由两个线程消费。