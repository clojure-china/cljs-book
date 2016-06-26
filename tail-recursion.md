
尾递归优化
----

### `recur`

尾递归优化是函数式编程不能缺少的一个性能优化方案.
没有尾递归, 常有的递归调用也会形成很深的调用栈消耗内存.
cljs 和 Clojure 类似, 都需要通过声明 `recur` 进行优化.
最终代码会被编译为 `white` 结构的 js 代码,从而提高性能.

```clojure
(defn factorial [acc n]
  (if (<= n 1) acc
    (recur (* acc n) (- n 1))))

(factorial 1 10)
```

### `trampoline`

`recur` 只能对当前函数进行尾递归, 如果尾递归涉及到多个函数,
需要借助新的函数作为跳板:

https://clojuredocs.org/clojure.core/trampoline
