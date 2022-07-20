# Reproducing an issue in Google Clojure Compiler

## Working in ES 6

```
rm -rf .cljs_node_repl ; \
clj -M --main cljs.main --target node --output-to main-es6.js -co "{:language-out :es6}" --compile main && \
node main-es6.js
```

## Broken in ES 5

```
rm -rf .cljs_node_repl ; \
clj -M --main cljs.main --target node --output-to main-es5.js -co "{:language-out :es5}" --compile main && \
node main-es5.js
```
