
JavaScript 模块
----

### 前端

shadow-cljs 当中对 npm 模块有比较成熟的支持, 通过 `ns` 可以声明依赖:

```clojure
(ns app.main (:require ["fs" :as fs]))

(fs/readFileSync "package.json" "utf8")
```

注意这里 `fs/` 用的是 `/` 表示 `fs` 类似命名空间.

旧的教程里会推荐 http://cljsjs.github.io/ 项目, 但是现在建议转用 shadow-cljs 的写法.
官方的 ClojureScript 对 `:npm-deps` 已经有越来越好的支持, 未来趋向于更好借助 npm 的资源.

### 后端

使用 Lumo 运行 ClojureScript 脚本时可以通过 `js/require` 调用 npm 模块.
另外 ClojureScript 编译后端代码生成的 js 文件也可以直接使用 `js/require`.
