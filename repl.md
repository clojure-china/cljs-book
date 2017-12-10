
REPL
----

除了 Lumo, 还有其他一些工具提供 REPL.

### Clojure CLI

在 Clojure 1.9 当中有了 CLI 的支持, 可以通过 brew 安装:

```bash
brew install clojure
```

创建一个 `deps.edn` 文件, 定义模块依赖:

```edn
{:deps {org.clojure/clojurescript {:mvn/version "1.9.946"}}}}
```

通过 `clj` 命令行启动, 使用 `-m` 参数指定默认运行的 module:

```bash
clj -m cljs.repl.node
```

[参考 Twitter](https://twitter.com/mfikes/status/939232383626342400).

### Planck

一个 macOS 环境的 REPL: http://planck-repl.org/

```bash
brew install planck
```

cljs 其实是自举完成的, 所以有时候可以脱离 JVM 作为编译器直接运行.
现在也可以运行在的 Windows 和 Linux, 然而安装方式我不清楚.

###  shadow-cljs

可以直接启动 ClojureScript REPL:

```bash
shadow-cljs cljs-repl
```

也可以基于 JVM 启动一个 Clojure 的 REPL:

```bash
shadow-cljs clj-repl
```

shadow-cljs 在 REPl 方面的功能相对 Lumo 少很多.

### npm 用户

有特别的需求的话, 也可以安装一下 npm 版本的 cljs,
提供了运行 cljs 的 API. 也有个 REPL.
考虑到 Planck 的 REPL 更优秀, 一般直接用 Planck.

https://www.npmjs.com/package/clojurescript
