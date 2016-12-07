
JavaScript 模块
----

### 前端

ClojureScript 依赖命名空间, 所以不能直接使用 npm 模块, 甚至 UMD 模块.
使用前需要做打包处理, 或者通过暴露在 `window` 对象的属性来调用.
已经打包的模块可以参考:

http://cljsjs.github.io/

### 后端

使用 Lumo 运行 ClojureScript 脚本时可以通过 `js/require` 调用 npm 模块.
另外 Figwheel 编译后端代码生成的 js 文件也可以直接使用 `js/require`.
