
Code Splitting
----

shadow-cljs 支持 Code splitting, 以及 Long term caching, 参考这个例子:
https://github.com/minimal-xyz/minimal-shadow-cljs-release

```edn
{:source-paths ["src/"]
 :dependencies []
 :builds {:app {:output-dir "dist/"
                :target :browser
                :asset-path "."
                :modules {:main {:entries [app.main]
                                 :depends-on #{:lib}}
                          :lib {:entries [app.lib]}}
                :release {:module-hash-names true}}}}
```

其中 `:modules` 配置中指定打包最终会生成 `main.js` 和 `lib.js` 两个文件.
以及 HTML 中需要指定 `lib` 需要在 `main` 之前加载, 以保证依赖关系.

`:module-hash-names` 选项会在文件名上增加 MD5 信息.
