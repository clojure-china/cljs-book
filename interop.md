
JavaScript 互操作
----

调用宿主语言代码最直接的办法就是通过 interop.
JavaScript 的全局变量可以通过 `js` 命名空间访问.
对象的方法调用可以写成:

```clojure
(.log js/console "demo) ; console.log('demo')
```

访问对象的属性需要添加连字符:

```clojure
(.-name obj) ; obj.name
```

对象的实例化可以用 cljs 写, 注意结尾有点号:

```clojure
(js/Date.) ; new Date()
```

当然用 `new` 也不是不可以:

```clojure
(new js/Date) ; new Date
```

在一般用到 interop 比较局限. 但有时会用到复杂对象.
复合数据结构直接转换通过 `clj->js` `js->clj` 两个函数进行.

需要复杂的数据结构还有一些复杂的操作, 可以看这篇文章:

http://www.spacjer.com/blog/2014/09/12/clojurescript-javascript-interop/

以及这个视频:

https://lambdaisland.com/episodes/clojurescript-interop
