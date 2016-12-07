
热替换
----

在运行时替换代码, 主要是两类的:

* 从 REPL 当中刷新代码重新引入命名空间
* ClojureScript 编译工具自动替换代码

### `(require 'x.y :reload)`

跟 Clojure REPL 类似, ClojureScript 有命令行工具可以替换命名空间,
主要是 Planck 和 Lumo, 比如 Lumo:

```clojure
(require '[x.y :as y] :reload)
```

就可以重新编译 `x.y` 对应的代码(使用缓存的情况下也要注意缓存).
主要用在后端.

### `boot-reload`

https://github.com/adzerk-oss/boot-reload

Boot 插件用于实现基本的热替换功能.

### figwheel

https://github.com/bhauman/lein-figwheel

基于 Leiningen 实现的 ClojureScript 编译和热替换的工具.
