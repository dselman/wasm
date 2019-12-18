
# AssemblyScript

https://github.com/AssemblyScript/assemblyscript

Create a file `index.ts`

``` typescript
// The entry file of your WebAssembly module.
//declare function sayHello(): void;

export function add(a: i32, b: i32): i32 {
  return a + b;
}

export function mul(a: i32, b: i32): i32 {
  return a * b;
}
```

``` bash
npm run asbuild
```

Create a file `index.js`

``` javascript
const fs = require("fs");
const compiled = new WebAssembly.Module(fs.readFileSync(__dirname + "/build/optimized.wasm"));
const imports = {
  env: {
    abort(_msg, _file, line, column) {
       console.error("abort called at index.ts:" + line + ":" + column);
    }
  },
  main: {
    sayHello() {
      console.log("Hello from WebAssembly!");
    }
  }
};
Object.defineProperty(module, "exports", {
  get: () => new WebAssembly.Instance(compiled, imports).exports
});
```

Create a file `run.js`

``` javascript
const add = require('./index').add;
const mul = require('./index').mul;

const result = add(1,3) + mul(2,3);
console.log(result);
```
