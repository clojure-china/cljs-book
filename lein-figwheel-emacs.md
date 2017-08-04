Leiningen + Figwheel + Emacs 配置
----

Lein 通过命令行启动, 通过 `project.clj` 文件配置.
`project.clj` 实际上是一个 Clojure 脚本, 运行时被读取.

### Emacs `C-x C-e` eval last cljs sexp 的配置

* 1.在 `project.clj` 文件里面的 `:dependencies` 引入

```clojure

:dependencies [ ...
               [com.cemerick/piggieback "0.2.2-SNAPSHOT"]
                ... ]


```


* 2.修改 `project.clj` 文件里面的 `:figwheel`

```clojure

:figwheel {...
           :nrepl-port 7003
           :nrepl-middleware ["cemerick.piggieback/wrap-cljs-repl"]
           ...
           }

```



* 3.` lein figwheel` 启动nrepl, 用Emacs的Cider连接nrepl的7003端口,并在浏览器端打开项目的页面

在你的Emacs配置里面加入 cljs-client-start, cljs-eval-sexp函数, cider连接完成后,在cider连接的buffer里面执行 ` M-x cljs-client-start ` 并回车两次, 使得cider的cljs客户端连接上浏览器, 完成后你就可以执行 ` C-x C-e ` 执行cljs单个S表达式了

cljs-eval-sexp函数是方便快速查看cljs变量和简单的表达式测试用的, 快捷键是 ` M-" `


```elisp

(defun cljs-client-start ()
  (interactive)
  (progn
    (insert "(use 'figwheel-sidecar.repl-api)\n")
    (insert "(cljs-repl)\n")
    (sleep-for 2)
    (rename-buffer (replace-regexp-in-string " " " CLJS " (buffer-name)))
    )
  )

(defun cljs-eval-sexp (sexp)
  (interactive "sClJS-EVAL:")
  (cider-interactive-eval sexp)
  )
(define-key global-map (kbd "M-\"") 'cljs-eval-sexp)

```

