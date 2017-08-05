
单元测试
----

ClojureScript 的测试和 Clojure 语法类似, 通过 `cljs.test` 来提供.
首先需要引用下面这些函数或者 Macros:

```clojure
(ns my-project.tests
  (:require [cljs.test :refer-macros [deftest is testing run-tests]]))
```

然后可以定义一个测试:

```clojure
(deftest test-numbers
  (is (= 1 1)))
```

可以参考官方的 [Testing](https://clojurescript.org/tools/testing) 章节来了解细节.

最终测试通过 `run-tests` 来运行的. 不过也有可能测试框架当中集成了测试的调用代码.

### shadow-cljs

在 shadow-cljs 中可以使用 Node.js 程序运行的方式来加载运行测试代码, 比如:
https://github.com/minimal-xyz/minimal-shadow-cljs-test

或者 `shadow-cljs test` 直接一次运行测试.

### boot-test

完成一些配置之后, 可以通过 `boot test` 来运行测试, 参考:
https://github.com/adzerk-oss/boot-test#usage

### JVM

由于 `.cljc` 后缀的源码文件可以直接在 Clojure(Script) 两个环境加载, 所以可以用 Clojure 的工具链来测试.
