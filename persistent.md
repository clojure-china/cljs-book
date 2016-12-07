
不可变数据
----

ClojureScript 中默认采用不可变数据作为底层实现.

比如 Vector 的实现, 底层是一棵树, 通常在操作时能做到结构共享从而做到内存和性能的优化.
具体可以参考文章:
[part 1](http://hypirion.com/musings/understanding-persistent-vector-pt-1)
[part 2](http://hypirion.com/musings/understanding-persistent-vector-pt-2)
[part 3](http://hypirion.com/musings/understanding-persistent-vector-pt-3)

比如 List 的实现, 实际是上链表.

关于 HashMap HashSet 等其他的数据结构还需要查阅更多文档...
