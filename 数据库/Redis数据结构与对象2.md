# Redis数据结构与对象-

## 跳表

跳表是一种**有序**的数据结构，支持平均$O(logN)$、最坏$O(N)$复杂度的节点查找，还能顺序操作处理节点，大部分情况下，效率与平衡树差不多且更加简单，更容易实现

跳表是有序结合键的底层实现之一

Redis只在两个地方用到跳表，一个是有序集合键，另一个是在集群节点中用作内部数据结构

![一个跳表](https://cdn.konyue.site/image-20220525160203727.png)

图片左边是zskiplist结构：

- header、tail : 指向跳表的表头、表尾节点

- level : 记录当前跳表内层数最大的那个节点的层数
- length ： 记录跳表的长度

右边是四个 zskiplistNode结构

- 层（level） :  用L1,L2,L3等表示各层，每层都带2个属性，前进指针和跨度
- 后退（ backward ）指针： 用BW字样标记节点的后退指针，指向位于当前节点的前一个节点。用于从表尾向表头遍历时使用
- 分值（ score ）: 各个节点的1.0、2.0、3.0是节点保存的分值，节点分值按从小到大排列
- 成员对象（ obj ）: 各个节点中o1、o2、o3是节点所保存的成员对象

表头节点和其他节点的构造是一样的，也有上面的属性，只是并不会被用到所以图中没画



