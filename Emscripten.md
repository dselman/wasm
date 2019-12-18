# Compile using Emscripten

https://emscripten.org


Create a file `add.c`

```
#include "emscripten.h"

EMSCRIPTEN_KEEPALIVE
int add(int a, int b) {
  return a + b;
}

EMSCRIPTEN_KEEPALIVE
int mul(int a, int b) {
    return a * b;
}```


```
emcc add.c -o add2.wasm -O3
```

Create a file `module.mjs`

```
import * as example from './add2.wasm';
console.log(example.add(8, 5));
```

```
node --experimental-modules --experimental-wasm-modules module.mjs
```
