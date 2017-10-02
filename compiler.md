
编译过程
----

Clojure 语言本身是编译到 JVM Bytecode, 而 ClojureScript 则是编译到 JavaScript.

### Macros

Clojure(Script) 编译过程大概经历三个阶段:

* 读取: 经字符串, 将 Macro 进行展开
* 分析: 基于读取的符号构建 AST
* 生成: 产生目标输出, 比如编译到 JavaScript

![](http://farm6.staticflickr.com/5341/7110268565_de4998482b_n_d.jpg)

这个过程对于 Clojure 和 ClojureScript 来说类似, 细节参考 [Compilation Pipeline](http://blog.fogus.me/2012/04/25/the-clojurescript-compilation-pipeline/).

比如这样一段 ClojureScript 代码, [参考 Mike 的文章](http://blog.fikesfarm.com/posts/2017-08-17-closure-compiler-in-planck.html):

```clojure
(defn f [long-name]
  (let [process (fn [foo]
                  (str "abc" "def"
                    (+ 1 2 3) foo))]
    (process long-name)))
```

通过 ClojureScript 的编译器会被编译成:

```js
function foo$core$g(long_name) {
  var process = function(foo__$1) {
    return ["abc", "def",
      cljs.core.str.cljs$core$IFn$_invoke$arity$1(1 + 2 + 3),
      cljs.core.str.cljs$core$IFn$_invoke$arity$1(foo__$1)
    ].join("");
  };
  return process.call(null, long_name);
}
```

### Google Closure Compiler

对于 JavaScript 而言, 在上线之前仍然需要进行优化, 比如前端常用 Uglify 优化代码体积.
在 cljs 社区, 普遍使用 Google Closure Compiler 进行优化, 可以做一些更深层的优化, 可以得到:

```js
function(a) { return ["abcdef",
  cljs.core.str.cljs$core$IFn$_invoke$arity$1(6),
  cljs.core.str.cljs$core$IFn$_invoke$arity$1(a)].join("");
}
```

可以得到代码被进一步简化了, 甚至部分的代码被预先做了计算.

cljs 编译器生成的代码可读性并不是那么好, 在使用有些函数的情况下会更加难读.
cljs 生成的代码本身针对 Google Closure Compiler 优化, 并且严重依赖 Dead Code Elimination 功能来控制体积.

Google Closure Compiler 主要有 [4 个编译选项](https://developers.google.com/closure/compiler/docs/compilation_levels#simple_optimizations):

* `:none` 不做任何优化, 不合并文件
* `:whitespace` 去除空白, 合并文件
* `:simple` 合并文件, 重命名局部变量
* `:advanced` 合并文件, 去除无用代码, 压缩混淆代码

由于 Google Closure Compiler 基于 Java 实现, 所以大部分 cljs 编译过程依赖 JVM.
比如 Lein 和 Boot 就基于 JVM 环境运行, 而 shadow-cljs 会调用系统的 JVM.

另一种办法是把 cljs 的编译器整个编译到 JavaScript, 同时使用 Closure Compiler 的 JavaScript 版本.
这种情况当中使用的 cljs 称为 Self-hosted ClojureScript, 有时也叫 Bootstraped ClojureScript.
比如 Planck 和 Lumo 就用了 Self-hosted ClojureScript, 可以使用 Node.js 来编译 cljs.
使用 Self-hosted cljs 相对而言冷启动较快, 但编译速度较慢, 适合在 REPL 中使用.
不过在 Self-hosted cljs 当中某些语言特性的细节会不同, 比如 Macro 的用法等等.
