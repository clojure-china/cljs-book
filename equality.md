
等价
----

cljs 的数据结构是在 js 基础之上实现的. 数值类型的数据可以直接判断.
一般通过 `(= a b)` 判断 `a` 和 `b` 的内容是否一致.
Collection 类型数据除了 `=` 函数之外,
还可以使用 `identical?` 函数判断两个数据的引用是否一致.

```clojure
(identical? {} {})
; true
(identical? {:a 1} {:a 1})
; false
(= {:a 1} {:a 1})
; true
(def a {a 1})
; #'cljs.user/a
(identical? a a)
; true
```

判断引用所需要的步骤往往很少, 所以几乎没有多少开销.
而递归判断内容一致很可能需要对数据结构进行遍历, 影响性能.
