
数据类型
----

可以通过 `(type x)` 来获取 `x` 的类型.

### 来自 JavaScript 的数据类型

* `nil`, 对应 `null`
* Number
* Boolean
* String
* RegExp

cljs 当中正则的语法是 `#"\\d"` 对应 js 里 `/\d/`.

`\d` 本来是字符类型, 在 js 环境中成了 String.

### ClojureScript 其他常用的类型

* Keyword, `:demo`, 或者从 String 生成 `(keyword "demo")`.
* Symbol, `'demo`, 或者从 String 生成 `(symbol "demo")`.
* Atom, `(atom 1)`, 这个写法实际上是把 Number 放进 Atom 里边.
* Vector, `[1 2 3 4]`. 也可以写成 `(vector 1 2 3 4)`.
* List, `'(1 2 3 4)`, 单引号. 也可以写成 `(list 1 2 3 4)`.
* HashMap, `{:a 1 :b 2}`. 也可以写成 `(hash-map :a 1 :b 2)`.
* HashSet, `#{1 2 3 4}`, 元素是唯一的. 也可以写成 `(hash-set 1 2 3 4)`.

在 ClojureScript 当中还有其他一些可是使用的列表类型.

可以用内置函数来判断类型:

```clojure
(string? "x")
; true
(keyword :a)
; :a
(number? 1)
; true
(boolean? true)
; true
(some? nil)
; false
(nil? nil)
; true
(fn? (fn []))
; true
```

### 类型转换

String:

```clojure
(str :a)
; ":a"
(str 1)
; "1"
(name :a)
; "a"
```

Keyword:

```clojure
(keyword "a")
; :a
```

Boolean:

```clojure
(boolean "true")
; true
(boolean 1)
; true
```

Number:

```clojure
(js/parseInt "11")
; 11
(js/parseFloat "11")
; 11
```

### 自定义类型

通过 `defrecord` 可以定义新的类型, 不过本质上是 HashMap:

```clojure
(defrecord Address [street city state zip])
; cljs.user/Address
```

实现一个实例:

```clojure
(Address. "200 N Mangum" "Durham" "NC" 27701)
; #cljs.user.Address{:street "200 N Mangum", :city "Durham", :state "NC", :zip 27701}
```

由于同时会生成对应的 Macro, 用 `->Address` 也是一样的:

```clojure
(->Address "200 N Mangum" "Durham" "NC" 27701)
; #cljs.user.Address{:street "200 N Mangum", :city "Durham", :state "NC", :zip 27701}
```
