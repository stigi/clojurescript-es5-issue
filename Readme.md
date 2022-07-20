# Reproducing an issue in Google Clojure Compiler

## Standard ClojureScript compiler
### Broken in ES 5

```
rm -rf .cljs_node_repl ; \
clj -M --main cljs.main --target node --output-to main-es5.js -co "{:language-out :es5}" --compile main && \
node main-es5.js
```

### Working in ES 6

```
rm -rf .cljs_node_repl ; \
clj -M --main cljs.main --target node --output-to main-es6.js -co "{:language-out :es6}" --compile main && \
node main-es6.js
```


## Shadow-CLJS

### Broken in ES 5

```
npx shadow-cljs compile es5 && node main-shadow-es5.js
```

### Working in ES 6

```
npx shadow-cljs compile es6 && node main-shadow-es6.js
```
