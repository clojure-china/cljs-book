
命名空间
----

由于 js 环境极少命名空间管理模块, namespace 相对陌生,
比如有这样的文件结构,

```text
src/
  demo/
    core.cljs
```

可以看到 `core.cljs` 的路径就是:

```bash
src/demo/core.cljs
```

注意 JVM 环境有个 classpath 的环境变量, 用于判断怎样查找源码,
classpath 对应多个路径, 也可能是 jar 包, 而 jar 包中也是源码,
对应到这里, 一般 `src/` 路径就在 classpath 当中,
然后路径跟命名空间是对应的, 所以 `core.cljs` 中定义的命名空间就是:

```clojure
(ns demo.core)
```

如果命名空间中存在连字符 `a-b.core`, 文件名需要特殊处理 `a_b/core.cljs`.
否则编译过程当中会提示错误, 说文件找不到, 其实是特殊字符的坑.

当前命名空间的依赖这样写:

```clojure
(ns demo.core
  (:require [clojure.string :as string]
            [clojure.set :refer [dfference]]))

(println (string/blank? ""))
(println (difference #{:a} #{:b}))
```
