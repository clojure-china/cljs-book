
安装
----

### Java

目前 cljs 的开发环境基于 Clojure, 也就是说需要 JVM.
大概有相当多办法可以安装 Java, 我是从官网直接下载安装的:

http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html

### Boot

Boot 是一个建构工具 http://boot-clj.com/

```bash
brew install boot-clj
```

类似 Gulp, 基于 task 进行组合以及运行, 社区有一些常用插件:

https://github.com/boot-clj/boot/wiki/Community-Tasks

### Planck

一个 macOS 环境的 REPL: http://planck-repl.org/

```bash
brew install planck
```

cljs 其实是自举完成的, 所以有时候可以脱离 JVM 作为编译器直接运行.
现在也可以运行在的 Windows 和 Linux, 然而安装方式我不清楚.

### npm 用户

有特别的需求的话, 也可以安装一下 npm 版本的 cljs,
提供了运行 cljs 的 API. 也有个 REPL.
考虑到 Planck 的 REPL 更优秀, 一般直接用 Planck.

https://www.npmjs.com/package/clojurescript


### Leiningen 用户

Leiningen 是另一个更早的建构工具, 简称 `lein` http://leiningen.org/

lein 更像是 Grunt, 配置强大, 然而 Boot 却很容易对 Task 进行组合使用.
对应 cljs 项目来说, 还是推荐用 Boot.

```clojure
brew install leiningen
```
