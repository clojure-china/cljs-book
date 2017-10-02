
安装运行
----

ClojureScript 的编译依赖 Java, 后来逐渐完成了 JavaScript 实现的 Self-hosted ClojureScript, 也就是能在 JavaScript 环境当中直接编译 ClojureScript.

这份文档当中使用 Lumo 作为 REPL 和脚本的执行工具, 使用 shadow-cljs 作为项目的建构工具.

### Lumo

一个基于 Self-hosted ClojureScript 开发的运行在 V8 的环境 https://github.com/anmonteiro/lumo

```bash
brew install lumo
```

Lumo 借助 V8 的 Snapshot 特性优化了启动速度. 同时支持在运行时引用 npm 模块. 后来 Lumo 也加入了 ClojureScript 建构的功能.

它的使用体验类似 `node`, 可以直接启动 REPL:

```bash
$ lumo
Lumo 1.4.1
ClojureScript 1.9.521
Node.js v7.9.0
 Docs: (doc function-name-here)
 Exit: Control+D or :cljs/quit or exit

cljs.user=> (println "demo")
demo
nil
cljs.user=>
```

也可以用 Lumo 运行脚本, 比如 `demo.cljs` 文件:

```clojure
(println "this is a demo")
(println (+ 1 2))
(def a 1)
(println a)
```

可以命令运行执行:

```bash
lumo demo.cljs
```

### shadow-cljs

shadow-cljs 是专为 ClojureScript 开发定制的精简的编译器, 提供了一些对非 Java 用户而言相对友好的功能 https://github.com/thheller/shadow-cljs

可以通过 npm 直接安装:

```bash
npm install -g shadow-cljs
```

shadow-cljs 使用 `shadow-cljs.edn` 作为配置文件, 比如:

```edn
{:source-paths ["src"]
 :dependencies []
 :builds {:app {:output-dir "target/"
                :asset-path "."
                :target :browser
                :modules {:main {:entries [app.main]}}
                :devtools {:after-load app.main/reload!}}}}
```

运行 `watch` 子命令的表示启动开发环境, 同时监视 `src/` 目录中的代码改变, 激活热替换功能:

```bash
shadow-cljs watch app
```

运行 `release` 子命令可以编译优化整个项目:

```bash
shadow-cljs release app
```

这里的 `app` 对应配置当中的 build-id `:app`.

shadow-cljs 运行中需要 Java 环境, 建议在系统当中安装 Java:

http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html

### 其他方案

其他的 REPL 环境还有 planck. 其他 cljs 编译方案也有基于 Boot, Lein, 甚至也可以直接调用 Java API 进行编译.
如果需要, 可以查询相关资料尝试.
