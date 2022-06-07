---
theme: ./theme
highlighter: shiki
monaco: false
---

# 前端模块化方案分享

<p class="pl-160 text-25px">
  —— Knight Chen
</p>

---

<div class="h-full flex items-center justify-center">
    <span class="text-30px">为什么要模块化？</span>
</div>

---

# 前端模块化方案

- IIFE (Immediately Invoked Function Expression)
- ~~CMD (Common Module Definition - SeaJS)~~
- ~~AMD (Asynchronous Module Definition - RequireJS)~~
- CJS (CommonJS - node)
- UMD (Universal Module Definition)
- ESM (ECMAScript)
- ~~SystemJS~~

---

# IIFE (Immediately Invoked Function Expression)

> 立即调用函数表达式

- 代码格式

  ```ts
  (function (win) {
    var JQuery = {};

    JQuery.ajax = {};

    win.$ = win.JQuery = JQuery;
  })(window);
  ```

- 使用方式

  ```html
  <script type="text/javascript" src="/path/to/jquery.js"></script>
  <script>
    $.ajax.post('/api.json');
  </script>
  ```

---

# CJS (CommonJS - node)

<div class="flex">
<div class="flex-1 pr-10">

- 模块定义

  ```js
  // knight.js
  const age = 18;
  const name = 'Knight Chen';

  module.exports = { name, age };
  ```

- 模块使用

  ```js
  // main.js
  const { age, name } = require('./knight');

  console.log(age); // 18
  console.log(name); // Knight Chen
  ```

</div>
<div class="flex-2 pl-10">

- cjs 的后缀通常为 `.js`, `.cjs`
- 早期，cjs 模块化方案只能在 node 平台中运行
- webpack 通过编译的手段，将其迁移到了 browser 环境中

编译之后格式如下:

```js
(function (modules) {
  // ...
  return __webpack_require__((__webpack_require__.s = 1));
})({
  './knight.js': function (module, exports, __webpack_require__) {
    const age = 18;
    const name = 'Knight Chen';

    module.exports = { name, age };
  },
  './main.js': function (module, exports, __webpack_require__) {
    const { age, name } = __webpack_require__('./knight');
    console.log(age); // 18
    console.log(name); // Knight Chen
  },
});
```

</div>
</div>

---

# UMD (Universal Module Definition)

- 由于现有模块化方案较多，难以统一
- umd 将现有市面上的模块化方案整合，一份代码可以同时适配多种模块化方案
- 通常包含的格式：`iife`, `amd`, `cjs`

<div class="flex">
<div class="flex-1 pr-10">

- 代码格式(cjs)

  ```js
  const age = 18;
  const name = 'Knight Chen';
  module.exports = { name, age };
  ```

</div>

<div class="flex-2 pl-10">

- 编译结果

  ```js
  (function (global, factory) {
    typeof exports === 'object' && typeof module !== 'undefined'
      ? factory(exports)
      : typeof define === 'function' && define.amd
      ? define(['exports'], factory)
      : ((global = typeof globalThis !== 'undefined' ? globalThis : global || self),
        factory((global.Kui = {})));
  })(this, function (exports) {
    const age = 18;
    const name = 'Knight Chen';
    exports.age = age;
    exports.name = name;
  });
  ```

</div>
</div>
---

# ESM (ECMAScript)

- ECMAScript 标准中定义的 js 模块化方案
- 使用 `import` 导入模块，`export` 导出模块
- 构建后的文件后缀通常为 `.mjs`

- 导出模块

  ```ts
  // knight.js
  const name = 'Knight Chen';
  const age = 18;
  export { name, age };
  ```

- 导入模块

  ```ts
  import { name. age } from './knight';

  console.log(age); // 18
  console.log(name); // Knight Chen
  ```

---

# ESM 与其他模块转换（CJS）

import { X } from 的适配

<div class="flex">
<div class="flex-1 pr-10">

```ts
import { name, age } from './knight';
console.log(name, age);
```

</div>
<div class="flex-1 pl-10">

```ts
const A = require('./knight');
console.log(A.name, A.age);
```

</div>
</div>

import \* as XXX 的适配

<div class="flex">
<div class="flex-1 pr-10">

```ts
import * as A from './knight';
```

</div>
<div class="flex-1 pl-10">

```ts
const A = require('./knight');
```

</div>
</div>

import XXX from 的适配

<div class="flex">
<div class="flex-1 pr-10">

```ts
import A from './knight';
```

</div>
<div class="flex-1 pl-10">

```ts
const A = require('./knight').default;
```

</div>
</div>

export default 的适配

<div class="flex">
<div class="flex-1 pr-10">

```ts
const name = 'Knight Chen';
const age = 18;
export default { name, age };
```

</div>
<div class="flex-1 pl-10">

```ts
const name = 'Knight Chen';
const age = 18;
exports.default = { name, age };
```

</div>
</div>

---

# 模块化方案选择

- IIFE: 需要在浏览器中通过 &lt;script src="/path/to/\*.js">的方式使用时

- CJS: 需要在 node 环境中使用时，通常为一些 nodejs 服务端的包，或者支持 ServerRender 的 组件库

- UMD: 需要同时支持 iife, cjs, amd 的包，通常体积较小

- ESM: 现阶段主流的模块化方案，可以被所有打包工具识别

> node 端使用就用 cjs, 浏览器端使用就用 esm, 支持 script 标签可用就使用 umd

---
layout: cover
---

# 谢谢观看
