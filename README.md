# WebAssembly Resources

Spec (Design Goals):
https://webassembly.github.io/spec/core/intro/introduction.html#design-goals

Introduction:
https://nxxm.github.io/cppcon2018/CPP_EVERYWHERE_WITH_WASM.html

WAT Playground:
https://webassembly.github.io/wabt/demo/wat2wasm/

Loading WASM as an ES Module:
https://dev.to/sendilkumarn/loading-wasm-as-esm-in-nodejs-2gdb

WAT2WASM:

Create a file `add.wat`

```
(module
  (func $add (param $p1 i32) (param $p2 i32) (result i32)
    local.get $p1
    local.get $p2
    i32.add)
  (export "add" (func $add))
)
```

``` bash
brew install wabt
wat2wasm add.wat
```

Create a file `module.mjs`

``` javascript
import * as example from './add.wasm';
console.log(example.add(8, 5));
```

Run WASM code in Node.js 12.x

``` bash
node --experimental-modules --experimental-wasm-modules module.mjs
```
