# Reproducing an issue in Google Clojure Compiler

This Repo tries to demonstrate an issue in the Google Clojure Compiler that produces one of the following errors:

- `ReferenceError: $jscomp is not defined`
- `TypeError: $jscomp.inherits is not a function`
- `Property '$jscomp' doesn't exist`

## Standard ClojureScript compiler

### Broken in ES 5 💥

```
rm -rf .cljs_node_repl ; \
clj -M --main cljs.main --target node --output-to main-es5.js -co "{:language-out :es5}" --compile main && \
node main-es5.js
```

<details><summary>Output</summary>

<pre>
WARNING: main is a single segment namespace at line 1 /Users/ullrich/tmp/es5-inherits/src/main.cljs


/Users/ullrich/tmp/es5-inherits/.cljs_node_repl/goog/base.js:1099
      exports = moduleDef.call(undefined, exports);
                          ^
ReferenceError: $jscomp is not defined
    at /Users/ullrich/tmp/es5-inherits/.cljs_node_repl/goog/iter/es6.js:79:1
    at Object.goog.loadModule (/Users/ullrich/tmp/es5-inherits/.cljs_node_repl/goog/base.js:1099:27)
    at Object.<anonymous> (/Users/ullrich/tmp/es5-inherits/.cljs_node_repl/goog/iter/es6.js:1:20)
    at Module._compile (internal/modules/cjs/loader.js:1085:14)
    at Object.Module._extensions..js (internal/modules/cjs/loader.js:1114:10)
    at Module.load (internal/modules/cjs/loader.js:950:32)
    at Function.Module._load (internal/modules/cjs/loader.js:790:12)
    at Module.require (internal/modules/cjs/loader.js:974:19)
    at require (internal/modules/cjs/helpers.js:101:18)
    at global.CLOSURE_IMPORT_SCRIPT (/Users/ullrich/tmp/es5-inherits/.cljs_node_repl/goog/bootstrap/nodejs.js:88:13)
</pre>

</details>

### Working in ES 6

```
rm -rf .cljs_node_repl ; \
clj -M --main cljs.main --target node --output-to main-es6.js -co "{:language-out :es6}" --compile main && \
node main-es6.js
```

<details><summary>Output</summary>

<pre>
shadow-cljs - config: /Users/ullrich/tmp/es5-inherits/shadow-cljs.edn
[:es6] Compiling ...
[:es6] Build completed. (83 files, 0 compiled, 0 warnings, 0,92s)
Hello, World!
</pre>

</details>


## Shadow-CLJS

### Broken in ES 5 💥

`npx shadow-cljs compile es5 && node main-shadow-es5.js`

<details><summary>Output</summary>

<pre>
shadow-cljs - config: /Users/ullrich/tmp/es5-inherits/shadow-cljs.edn
[:es5] Compiling ...
[:es5] Build completed. (83 files, 0 compiled, 0 warnings, 1,40s)
SHADOW import error /Users/ullrich/tmp/es5-inherits/.shadow-cljs/builds/es5/dev/out/cljs-runtime/goog.iter.es6.js

/Users/ullrich/tmp/es5-inherits/main-shadow-es5.js:385
      exports = moduleDef.call(undefined, exports);
                          ^
TypeError: $jscomp.inherits is not a function
    at /Users/ullrich/tmp/es5-inherits/.shadow-cljs/builds/es5/dev/out/cljs-runtime/goog/iter/es6.js:144:32
    at Object.goog.loadModule (/Users/ullrich/tmp/es5-inherits/main-shadow-es5.js:385:27)
    at /Users/ullrich/tmp/es5-inherits/.shadow-cljs/builds/es5/dev/out/cljs-runtime/goog/iter/es6.js:1:1
    at global.SHADOW_IMPORT (/Users/ullrich/tmp/es5-inherits/main-shadow-es5.js:64:44)
    at /Users/ullrich/tmp/es5-inherits/main-shadow-es5.js:1552:1
    at Object.<anonymous> (/Users/ullrich/tmp/es5-inherits/main-shadow-es5.js:1593:3)
    at Module._compile (internal/modules/cjs/loader.js:1085:14)
    at Object.Module._extensions..js (internal/modules/cjs/loader.js:1114:10)
    at Module.load (internal/modules/cjs/loader.js:950:32)
    at Function.Module._load (internal/modules/cjs/loader.js:790:12)
</pre>

</details>

### Working in ES 6

`npx shadow-cljs compile es6 && node main-shadow-es6.js`

<details><summary>Output</summary>

<pre>
shadow-cljs - config: /Users/ullrich/tmp/es5-inherits/shadow-cljs.edn
[:es6] Compiling ...
[:es6] Build completed. (83 files, 0 compiled, 0 warnings, 0,92s)
Hello, World!
</pre>

</details>
