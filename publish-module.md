
发布模块
----

ClojureScript 的模块按照 Clojure 的习惯, 是通过 jar 包发布在 https://clojars.org/ 的.

Clojars 的教程涉及到一些复杂的内容. 我出于习惯使用已有的脚本来发布, 脚本运行时需要修改密码.

> 注意替换这个脚本当中的账户名和包名, 然后以 `build.boot` 文件通过 Boot 来执行.

```clojure
(defn read-password [guide]
  (String/valueOf (.readPassword (System/console) guide nil)))

(set-env!
  :resource-paths #{"src"}
  :dependencies '[]
  :repositories #(conj % ["clojars" {:url "https://clojars.org/repo/"
                                     :username "<YOUR_CLOJARS_USERNAME>"
                                     :password (read-password "Clojars password: ")}]))

(def +version+ "0.1.0")

(deftask deploy []
  (comp
    (pom :project     'your-namespace/your-pacakge
         :version     +version+
         :description ""
         :url         "https://github.com/your-org/your-package"
         :scm         {:url "https://github.com/your-org/your-package"}
         :license     {"MIT" "http://opensource.org/licenses/mit-license.php"})
    (jar)
    (install)
    (push :repo "clojars" :gpg-sign false)))
```

这个脚本跳过 GPG 密钥签名相关的操作, 如果你有需要请自行学习了解.
