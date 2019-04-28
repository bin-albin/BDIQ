# Spark常见知识点

#### 一：ReduceByKey和GroupByKey的区别是什么？

答：在对大数据进行复杂计算时，reduceByKey优于groupByKey

reduceByKey用于对每个key对应的多个value进行merge操作，最重要的是它能够在本地先进行merge操作，并且merge操作可以通过函数自定义

reduceByKey会在结果发送至reducer之前会对每个mapper在本地进行merge，有点类似于在MapReduce中的combiner。这样做的好处在于，在map端进行一次reduce之后，数据量会大幅度减小，从而减小传输，保证reduce端能够更快的进行结果计算。

![](../.gitbook/assets/image%20%281%29.png)

groupByKey会对每一个RDD中的value值进行聚合形成一个序列\(Iterator\)，此操作发生在reduce端，所以势必会将所有的数据通过网络进行传输，造成不必要的浪费。同时如果数据量十分大，可能还会造成OutOfMemoryError

![](../.gitbook/assets/image%20%282%29.png)

通过以上对比可以发现在进行大量数据的reduce操作时候建议使用reduceByKey。不仅可以提高速度，还是可以防止使用groupByKey造成的内存溢出问题

#### 二：Spark运行流程图，基于Yarn-cluster、Yarn-client、Standalone模式？

#### 三：spark是如何实现on yarn的？如何设计一个基于yarn调度的应用服务

四：Spark为什么比MR快？

五：RDD的宽依赖和窄依赖

六：为什么Spark Application在没有获得足够的资源，job就开始执行了，可能会导致什么什么问题发生？

七：cogroup rdd实现原理，你在什么场景下用过这个rdd

