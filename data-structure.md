
数据结构
----

大概下边几个结构都是基于 Sequence 实现的.

```clojure
(first coll)
(rest col)
(cons item seq)
```

http://clojure.org/reference/sequences

### List

### Vector

```clojure
(set a [1 2 3 4])
(get a 0)
(first a)
```

https://clojuredocs.org/clojure.core/vector

### HashMap

```clojure
(def b {:a 1 :b 2})
(get b :a)
(:b a)
(a :b)
```

https://clojuredocs.org/clojure.core/hash-map

### HashSet

https://clojuredocs.org/clojure.core/hash-set
