# 数据结构

## B Tree

## B+ Tree

## LSM Tree
LSM-Tree全称是Log Structured Merge Tree，是一种分层，有序，面向磁盘的数据结构，其核心思想是充分利用了磁盘批量的顺序写要远比随机写性能高出很多
> ![avatar](lsm-tree.jpeg)

> 写入过程：
> * 当收到一个写请求时，会先把该条数据记录在WAL Log里面，用作故障恢复
> * 当写完WAL Log后，会把该条数据写入内存的SSTable里面（删除是墓碑标记，更新是新记录一条的数据），也称Memtable。注意为了维持有序性在内存里面可以采用红黑树或者跳跃表相关的数据结构
> * 当Memtable超过一定的大小后，会在内存里面冻结，变成不可变的Memtable，同时为了不阻塞写操作需要新生成一个Memtable继续提供服务
> * 把内存里面不可变的Memtable给dump到到硬盘上的SSTable层中，此步骤也称为Minor Compaction，这里需要注意在L0层的SSTable是没有进行合并的，所以这里的key range在多个SSTable中可能会出现重叠，在层数大于0层之后的SSTable，不存在重叠key
> * 当每层的磁盘上的SSTable的体积超过一定的大小或者个数，也会周期的进行合并。此步骤也称为Major Compaction，这个阶段会真正 的清除掉被标记删除掉的数据以及多版本数据的合并，避免浪费空间，注意由于SSTable都是有序的，我们可以直接采用merge sort进行高效合并

> 读取过程：
> * 当收到一个读请求的时候，会直接先在内存里面查询，如果查询到就返回
> * 如果没有查询到就会依次下沉，知道把所有的Level层查询一遍得到最终结果