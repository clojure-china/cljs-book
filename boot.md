
Boot
----

Boot 通过命令行启动, 通过 `build.boot` 文件配置.
`build.boot` 实际上是一个 Clojure 脚本, 运行时被读取.

### task

任务, 大概相当于 Gulp 里的 task, 可以从命令行调用.
任务可以进行组合, 一次顺序执行多个任务.
简单的 task 可以通过这个 Macro 定义:

```clojure
(deftask null-task
  "Does nothing."
  []
  (fn [next-task]
    (fn [fileset]
      (next-task fileset))))
```

多个 task 可以通过 `comp` 函数组合然后执行:

https://github.com/boot-clj/boot/wiki/Tasks

### Boot environment

Boot 的环境变量, 通过 `set-env!` 进行修改, 常用的环境变量:

* `resource-paths` 作为源码输入, 也能够进入 jar 包里
* `source-paths` 作为源码输入, 但不能进入 jar 包里
* `asset-paths` 作为静态资源输入, 也能够进入 jar 包里
* `dependencies` 整个项目的依赖

完整的环境变量的列表参考 Wiki:

https://github.com/boot-clj/boot/wiki/Boot-Environment

### Java environment

大致相当于 Boot 的配置文件, 主要是一般可以是:

```clojure
=>> cat ~/.boot/boot.properties
#http://boot-clj.com
#Wed Mar 23 17:58:25 CST 2016
BOOT_CLOJURE_NAME=org.clojure/clojure
BOOT_CLOJURE_VERSION=1.8.0
BOOT_VERSION=2.5.5
BOOT_EMIT_TARGET=no
```

注意 `BOOT_EMIT_TARGET` 这个环境变量在 Boot 中有过大的调整.
原来 Boot 默认会输入内容到 target, 后来建议关闭这个行为.

https://github.com/boot-clj/boot/wiki/Configuring-Boot

### target

target 现在是一个 task, 运行 task 会把文件默认输出到 `target/` 路径.
target task 调用时可以通过 `:dir` 设置路径的位置, 但一般不用设置.

```clojure
(target :dir #{"compiled/"})
```

### fileset

大致可以认为是文件的集合, 也是 task 之间传递的主要内容.
从前面提到的 `source-paths` 等路径开始读取, 但根据参数不同而有不同特性.
其实 task 运行主要就是针对文件操作, 其中经常用到临时文件.
相对于 Gulp 使用文件流, Boot 使用的是 fileset 和临时文件.

https://github.com/boot-clj/boot/wiki/Filesets

### Options

定义 task 参数时, 可以通过这套 DSL 定义参数的名称和类型,
一般不写 task 或者插件不需要深入. 比较复杂, 需要看文档才能明白用途:

```clojure
(deftask options
  "Demonstrate the task options DSL."
  [a a-option VAL  kw    "The option."
   c counter       int   "The counter."
   e entry    VAL  sym   "An entrypoint symbol."
   f flag          bool  "Enable flag."
   o o-option VAL  str   "The other option."]
  *opts*)
```

https://github.com/boot-clj/boot/wiki/Task-Options-DSL

### 例子

一个编译 cljs 的简单配置, 编译 `src/` 里的文件到 `target/`:

```clojure
(set-env!
 :dependencies '[[org.clojure/clojurescript "1.9.36"      :scope "test"]
                 [org.clojure/clojure       "1.8.0"       :scope "test"]
                 [adzerk/boot-cljs          "1.7.170-3"   :scope "test"]])

(require '[adzerk.boot-cljs   :refer [cljs]])

(deftask build-advanced []
  (set-env!
    :source-paths #{"src"})
  (comp
    (cljs :optimizations :advanced)
    (target)))
```
