
变量
----

在一个命名空间中定义变量可以这样写, 下面的代码可以在 Lumo 当中试验:

```clojure
(def a 1)
; #'cljs.user/a
```

也有局部的绑定, 通过 `let` 来定义:

```clojure
(let [x 1
      y 2]
  (+ x y))
; 3
```

数据绑定之后, 一不可以修改.

在 cljs 环境里用到可变状态, 需要通过 `Atom` 类型定义可变状态:

```clojure
(def b (atom 1))
; #'cljs.user/b
```

`Atom` 类型是一个引用, 每次读取最新的数据时需要通过 `@b` 语法来取最新的值, 或者 `(deref b)`. 一般为了突出可变状态, 会使用 `*b` 这样的命名习惯. 这样定义和修改状态就是:

```clojure
(def *b (atom 1))
; #'cljs.user/b
(reset! *b 2)
; 2
```

由于前端经常使用热替换机制, 所以专门的函数, 避免热替换后重新计算绑定.
`defonce` 一般是和 `Atom` 类型配合使用:

```clojure
(defonce *c (atom 1))
; #'cljs.user/*c
```
