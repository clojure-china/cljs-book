
函数
----

### 基本定义

最简单的函数定义是:

```clojure
(defn f1 [x y]
  (+ x y))
; #'cljs.user/f1
```

借助匿名函数也可以函数定义, 不过这样可能损失一些静态检查的好处:

```clojure
(def f2 (fn [x y]
  (+ x y)))
; #'cljs.user/f2
```

如果函数参数个数不确定, 可以用 `&` 把后边的参数合并成一个 list:

```clojure
(defn f3 [x1 & xs]
  (print x1)
  (print xs))
; #'cljs.user/f3
```

根据参数个数的不同, 函数可以被重载:

```clojure
(defn f4 [x] (+ x 1))
; #'cljs.user/f4
(defn f4 [x y] (+ x y 1))
; #'cljs.user/f4
```

也可以简写在一个表达式当中:

```clojure
(defn f4
  ([x] (+ x 1))
  ([x y] (+ x y 1)))
; #'cljs.user/f4
```

### 调用函数

函数调用比较简单, 注意有个 `apply` 函数可以改变参数的传递方式:

```clojure
(f1 1 2)
; 3
(apply f1 (list 1 2))
; 3
```
