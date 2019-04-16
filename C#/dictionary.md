# Dictionary

## [Hash Table(Hash Map)](https://en.wikipedia.org/wiki/Hash_table)

Hash Table(Hash Map)就是一种可以实现键值对集合的数据结构，在这个集合中每个键最多出现一次。

## Hash Table(Hash Map)的实现

哈希方法会计算每个键，并把它们放入唯一的一个集合(bucket)
<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/d/d0/Hash_table_5_0_1_1_1_1_1_LL.svg/450px-Hash_table_5_0_1_1_1_1_1_LL.svg.png">

数据结构

    int[] buckets

    TValue[] entries

    struct entry {
        TKey;
        TValue;
        HashCode;
        Next;
    }

上图中John Smith, Lisa Smith等代表Key，经过哈希方法，这些Key被分配在buckets数组中，每个buckets数组的值是这个bucket现在指向的entry所在数组entries的下标，这些entry被存储在entries数组中。每个entry有一个属性，指向下一个entry。

## 怎么判断一个Key是否在Hash Table中

1. 输入一个Key
2. 将这个Key经过哈希方法得到它会被分配到哪个bucket中，即得到buckets数组的下标`i`
3. 然后通过`buckets[i]`可以得到当前这个bucket指向的entry
4. 通过第三步得到的entry和entry的next属性，循环就可以获得分配到这个bucket里的所有的entries
5. 对比某个bucket里面所有的entries的key和hashcode，就可以判断一个Key是否在Hash Table中

## 总结

* C# 中的Dictionary就是用两个数组实现了Hash Table这种数据结构
* 阅读C#的源码，当你一个空的Dictionary插入一个键值对时，会初始化大小为3个元素的两个数组，随着元素越来越多，还需要Resize这两个数组
* Dictionary是个类，所以是引用类型，会分配在堆上，堆上的对象越多，可能会触发垃圾收集，垃圾收集影响性能，因为它会把所有线程挂起