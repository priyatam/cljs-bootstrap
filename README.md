# cljs-bootstrap

Use ClojureScript to compile itself.

## Usage

Compile [Cljs](http://github.com/clojure/clojurescript) and
[tools.reader](https://github.com/clojure/tools.reader) from source and install
npm deps for decent stacktraces:

```bash
chmod a+x setup
./setup
```

Modify this repo's `project.clj` to reflect the Cljs version.

Start the REPL:

```
rlwrap lein trampoline run -m clojure.main script/repl.clj 
```

Try the following at the REPL by loading the necessary namespaces:

```clj
(require-macros '[cljs.env.macros :refer [ensure]])
(require '[cljs.analyzer :as ana] '[cljs.compiler :as c])
```

Now you can eval. 

```clj
(js/eval
  (with-out-str
    (c/emit
      (ensure
        (ana/analyze-keyword
          (assoc (ana/empty-env) :context :expr)
          :foo)))))
```

Currently only trivial expressions work. Arbitrary source code requires macro
support which has not yet landed in ClojureScript master.

## License

Copyright © 2015 David Nolen, Rich Hickey & Contributors

Distributed under the Eclipse Public License either version 1.0 or (at
your option) any later version.
