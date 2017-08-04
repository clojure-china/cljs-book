
不可变数据
----

ClojureScript 中默认采用不可变数据作为底层实现.

cljs 当中实现了 Persistent Data Structure,
虽然是不可变数据, 但创建新数据一般会进行结构复用,
也就是说, 比如下面这个例子, `b` 在内部实现中就可以复用 `a` 的某些部分

```clojure
(def a {:a 1 :b 2})
; #'cljs.user/a
(assoc a :c 3)
; {:a 1, :b 2, :c 3}
a
; {:a 1, :b 2}
```

比如 Vector 的实现, 底层是一棵树, 通常在操作时能做到结构共享从而做到内存和性能的优化.
具体可以参考文章:
[part 1](http://hypirion.com/musings/understanding-persistent-vector-pt-1)
[part 2](http://hypirion.com/musings/understanding-persistent-vector-pt-2)
[part 3](http://hypirion.com/musings/understanding-persistent-vector-pt-3)

比如 List 的实现, 实际是单链表.

关于 HashMap HashSet 等其他的数据结构还需要查阅更多文档...

有兴趣可以顺着链接继续翻[不可变数据][blog].

[blog]: https://segmentfault.com/a/1190000002957634
