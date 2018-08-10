##HashMap 源码分析
    HashMap 遍历的性能和 其实例的容量(capacity)和size大小成正比例关系，因此 如果需要遍历操作时，不应该把 **初始容量(initial capacity)** 设置的太高，或者把 **负载因子(load factor)**设置的太小

    An instance of HashMap has two parameters that affect its performance: initial capacity and load factor. The capacity is the number of buckets in the hash table, and the initial capacity is simply the capacity at the time the hash table is created. The load factor is a measure of how full the hash table is allowed to get before its capacity is automatically increased. When the number of entries in the hash table exceeds the product of the load factor and the current capacity, the hash table is rehashed (that is, internal data structures are rebuilt) so that the hash table has approximately twice the number of buckets.
    容量(capacity)是hash table 的大小，初始容量就是初始化HashMap市容量的大小，HashMap 默认的大小是1<<4,
    负载因子是测量hash table接近最大容量的多少会自动扩容(rehashed)，例如容量为16，当hash table的大小达到16 * 0.75 时就会自动扩容，默认的负载因子是0.75. 

>注意：**HashMap不是同步的**