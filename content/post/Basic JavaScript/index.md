---
title: "Basic JavaScript"
date: 2022-01-15T11:46:17+08:00
draft: false
lastmod: 
image: "cover.jpg"
categories:
    - Notes
tags:
    - JavaScript
    - Programming
---

## JavaScript高级程序设计（第4版）

### 第1章 什么是 JavaScript

#### JavaScript 实现

- 核心 (ECMAScript): 语法、类型、语句、关建字、保留字、操作符、全局对象
- 文档对象模型 (Document Object Model)：将整个 HTML 或 XML 网页内容抽象为一组包含不同的数据的分层节点，并以 DOM 视图、事件、样式、遍历和范围 API 的形式实现节点的删除、添加、替换、修改
- 浏览器对象模型 (Browser Object Model)：用于支持访问和操作浏览器的窗口的 API

### HTML 中的 JavaScript

#### `<script>` 元素

所有 `<script>` 元素依照出现次序被解释。浏览器解释完 `<script>` 中的代码才继续渲染页面的剩余部分。为此，通常应该把 `<script>` 元素放到页面主内容之后及 `</body>` 标签之前。

- `src`：表示包含要执行的代码的外部文件。
- `async`：立即开始下载脚本，但不能阻止其他页面动作，比如下载资源或等待其他脚本加载。只对外部脚本文件有效。异步脚本不应该在加载期间修改 DOM。
- `defer`：脚本可以延迟到文档完全被解析和显示之后再按列出的顺序执行。只对外部脚本文件有效。
- `crossorigin`：配置相关请求的 CORS（跨源资源共享）设置。默认不使用 CORS。`crossorigin="anonymous"` 配置文件请求不必设置凭据标志。`crossorigin="use-credentials"` 设置凭据标志，意味着出站请求会包含凭据。
- `integrity`：允许比对接收到的资源和指定的加密签名以验证子资源完整性（SRI，Subresource Integrity）。如果接收到的资源的签名与这个属性指定的签名不匹配，则页面会报错，脚本不会执行。这个属性可以用于确保内容分发网络（CDN，Content Delivery Network）不会提供恶意内容。
- `type`：表示代码块中脚本语言的内容类型（也称MIME 类型）。按照惯例，这个值始终都是 `"text/javascript"`，尽管 `"text/javascript"` 和 `"text/ecmascript"` 都已经废弃了。JavaScript 文件的MIME 类型通常是 `"application/x-javascript"`，不过给 `type` 属性这个值有可能导致脚本被忽略。在非 IE 的浏览器中有效的其他值还有 `"application/javascript"` 和 `"application/ecmascript"`。如果这个值是 `module`，则代码会被当成 ES6 模块，而且只有这时候代码中才能出现 `import` 和 `export` 关键字。

##### 动态加载脚本

```javascript
let script = document.createElement('script');
script.src = 'gibberish.js';
script.async = false;
document.head.appendChild(script);
```

```html
<link rel="preload" href="gibberish.js">
```

#### `<noscript>` 元素

### 第3章 语言基础

#### 语法

- 区分大小写
- 标识符以 `字母`/`_`/`$` 开始，驼峰表示，可使用 Unicode 字母字符
- `//` 单行注释，`/* */` 多行注释
- `"use strict";` 预处理指令启用严格模式
- 句尾应加 `;`（即使非必须）
- `{ }` 合并多条语句的代码块

#### 关键字

- `break` `do` `in` `typeof` `case` `else` `instanceof` `var` `catch` `export` `new` `void` `class` `extends` `return` `while` `const` `finally` `super` `with` `continue` `for` `switch` `yield` `debugger` `function` `this` `default` `if` `throw` `delete` `import` `try`
- `enum`
- 严格模式下 `implements` `package` `public` `interface` `protected` `static` `let` `private`
- 模块代码中 `await`

#### 变量声明

1. `const`：**块**作用域；声明变量时**必须**同时初始化变量；**不能**修改声明的变量（若变量引用的是一个对象，修改对象内部的属性是允许的）
2. `let`：**块**作用域；**不允许**同一块作用域中重复声明（可以嵌套使用）；**不会**在作用域中被提升，产生暂时性死区（temporal dead zone）；在全局作用域中声明的变量**不会**成为 `window` 对象的属性；**不能**使用条件式声明，`for` 循环定义的迭代变量不会渗透到循环体外部
3. <del>`var`：**函数**作用域；去掉 `var` 操作符定义全局变量，严格模式中会抛出 `ReferenceError`；严格模式中不能定义名为 `eval` / `arguments` 的变量；声明的变量会自动提升（hoist）到函数作用域顶部；允许重复声明（在作用于顶部合并）</del>

#### 数据类型

- 简单数据类型 / 原始类型：`Undefined`、`Null`、`Boolean`、`Number`、`String`、`Symbol`
- 复杂数据类型：`Object`

`typeof` 操作符返回字符串：

- `"undefined"` 表示值未定义（使用 `var` 或 `let` 声明了变量但没有初始化），是一个假值

  ```javascript
  let message; // 这个变量被声明了，只是值为undefined
  // 确保没有声明过这个变量
  // let age
  console.log(message); // "undefined"
  console.log(age); // 报错
  
  let message; // 这个变量被声明了，只是值为undefined
  // 确保没有声明过这个变量
  // let age
  console.log(typeof message); // "undefined"
  console.log(typeof age); // "undefined"
  ```

  未初始化的变量会被自动赋予 `undefined` 值，应在声明变量的同时进行初始化，以便判断返回 `"undefined"` 的 `typeof` 是给定的变量尚未声明还是声明了但未初始化。

- `"boolean"` 表示值为布尔值

  `Boolean()` 转型函数转换规则：

  | 数据类型    | 转换为 `true` 的值     | 转换为 `false` 的值 |
  | ----------- | ---------------------- | ------------------- |
  | `Boolean`   | `true`                 | `false`             |
  | `String`    | 非空字符串             | `""`（空字符串）    |
  | `Number`    | 非零数值（包括无穷值） | `0`、`NaN`          |
  | `Object`    | 任意对象               | `null`              |
  | `Undefined` | `N/A`（不存在）        | `undefined`         |

- `"number"` 表示值为数值

  - 使用 IEEE 754 格式表示整数和浮点值，存在浮点舍入错误

  - `0` / `0o` 数值前缀表示八进制字面量（`0` 在严格模式下无效），`0x` 表示十六进制字面量

  - `.1` 有效但不推荐

  - `1.` / `10.0` 会被转化成整数

  - 支持科学计数法表示 `3.125e7`，小数点后至少包含六个零的浮点值将被转换为科学计数法

  - 可表示的范围为 `Number.MIN_VALUE` ~ `Number.MAX_VALUE`，超出则会转化为`Number.NEGATIVE_INFINITY` 或 `Number.POSITIVE_INFINITY` 属性中的 `Infinity` / `-Infinity`，如 $\frac{有符号 0 或无符号 0}{非 0}$，使用 `isFinite()`判断

  - `NaN` 意为 Not a Number，表示本来要返回数值的操作失败了，如除 0

    - 任何涉及 `NaN` 的操作始终返回 `NaN`
    - `NaN` 不等于包括 `NaN` 在内的任何值
    - 任何不能转化为数值的值都会导致 `isNaN()` 函数返回 `true`

  - 数值转换

    - 转型函数 `Number()`

      > 一元加操作符与Number()函数遵循相同的转换规则。

      | 参数        | 返回值                                                       |
      | ----------- | ------------------------------------------------------------ |
      | 布尔值      | `true` 转换为 `1`，`false` 转换为 `0`                        |
      | 数值        | 直接返回                                                     |
      | `null`      | 返回 `0`                                                     |
      | `undefined` | 返回 `NaN`                                                   |
      | 字符串      | 如果包含数值字符，包括数值字符前面带加、减号的情况，则转换为一个十进制数值（`Number("011")` 忽略前面的零返回 `11`）；如果包含有效的浮点值格式如 `"1.1"`，则会忽略前面的零转换为相应的浮点值；如果包含有效的十六进制格式如 `"0xf"`，则会转换为与该十六进制值对应的十进制整数值；如果是 `""`，则返回 `0`； 如果包含除上述情况之外的其他字符，则返回 `NaN` |
      | 对象        | 调用 `valueOf()` 方法，并按照上述规则转换返回的值；如果转换结果是 `NaN`，则调用 `toString()` 方法，再按照转换字符串的规则转换 |

    - `parseInt()` 函数

      - 忽略字符串最前面的空格，从第一个非空格字符开始转换；如果第一个字符不是数值字符、加号或减号，立即返回 `NaN`（因此 `""` 会返回 `NaN`）；否则继续依次检测每个字符，直到字符串末尾，或碰到非数值字符（不同的整数格式前缀除外，亦可传入第二个参数指定进制数）
      - 为避免解析出错，应始终传入第二个参数

    - `parseFloat()` 函数

      - 类似 `parseInt()` 函数，支持包括科学计数法在内的所有浮点格式
      - 第二次出现的小数点及以后的剩余字符都会被忽略
      - 始终忽略字符串开头的零
      - 仅十进制

- `"string"` 表示值为字符串

  - 字符串以`'` / `"` / `` ` `` 表示，是不可改变的

  - 字符字面量

    | 字面量   | 含义                                                         |
    | -------- | ------------------------------------------------------------ |
    | `\n`     | 换行                                                         |
    | `\t`     | 制表                                                         |
    | `\b`     | 退格                                                         |
    | `\r`     | 回车                                                         |
    | `\f`     | 换页                                                         |
    | `\\`     | 反斜杠                                                       |
    | `\'`     | 单引号                                                       |
    | `\"`     | 双引号                                                       |
    | ``\` ``  | 反引号                                                       |
    | `\xnn`   | 以十六进制编码 `nn` 表示的字符（其中 `n` 是十六进制数字 `0~F`），例如 `\x41` 等于 `"A"` |
    | `\unnnn` | 以十六进制编码 `nnnn` 表示的 Unicode 字符（其中 `n` 是十六进制数字 `0~F`），例如 `\u03a3` 等于希腊字符 `"Σ"` |

  - 字符串的长度可以通过其 `length` 属性获取

    > 如果字符串中包含双字节字符，那么length 属性返回的值可能不是准确的字符数。
    > 第 5 章将具体讨论如何解决这个问题
    >

  - `toString()` 方法转换为字符串

    - `null` 和 `undefined` 值没有 `toString()` 方法，可使用 `String()` 转型函数：

      - 如果值有 `toString()` 方法，则调用该方法（不传参数）并返回结果

      - 如果值是 `null`，返回 `"null"`

      - 如果值是 `undefined`，返回 `"undefined"`

        >  用加号操作符给一个值加上一个空字符串 `""` 也可以将其转换为字符串

    - 对数值调用时，可接受底数参数

  - 模板字面量：`` ` `` 保留换行字符，保持内部的空格

    - 字符串插值：所有以 `${}` 插入的值都会使用 `toString()` 强制转型为字符串，而且任何JavaScript 表达式都可以用于插值

      ```javascript
      let value = 5;
      let exponent = 'second';
      // 以前，字符串插值是这样实现的：
      let interpolatedString = value + ' to the ' + exponent + ' power is ' + (value * value);
      // 现在，可以用模板字面量这样实现：
      let interpolatedTemplateLiteral = `${ value } to the ${ exponent } power is ${ value * value }`;
      console.log(interpolatedString); // 5 to the second power is 25
      console.log(interpolatedTemplateLiteral); // 5 to the second power is 25
      ```

    - 标签函数：接收被插值记号分隔后的模板和对每个表达式求值的结果

      ```javascript
      let a = 6;
      let b = 9;
      
      function simpleTag(strings, ...expressions) {
        console.log(strings);
        for(const expression of expressions) {
        	console.log(expression);
      	}
      	return 'foobar';
      }
      
      function zipTag(strings, ...expressions) {
      	return strings[0] + expressions.map((e, i) => `${e}${strings[i + 1]}`).join('');
      }
      
      let untaggedResult = `${ a } + ${ b } = ${ a + b }`;
      let taggedResult = simpleTag`${ a } + ${ b } = ${ a + b }`;
      // ["", " + ", " = ", ""]
      // 6
      // 9
      // 15
      let zipTaggedResult = zipTag`${ a } + ${ b } = ${ a + b }`;
      
      console.log(untaggedResult); // "6 + 9 = 15"
      console.log(taggedResult); // "foobar"
      console.log(zipTaggedResult); // "6 + 9 = 15"
      ```

    - 原始字符串：使用 `String.raw` 标签函数获取原始的模板字面量内容（如换行符或 Unicode 字符），而不是被转换后的字符表示

      ```javascript
      // Unicode 示例
      // \u00A9 是版权符号
      console.log(`\u00A9`); // ©
      console.log(String.raw`\u00A9`); // \u00A9
      // 换行符示例
      console.log(`first line\nsecond line`);
      // first line
      // second line
      console.log(String.raw`first line\nsecond line`); // "first line\nsecond line"
      // 对实际的换行符来说是不行的
      // 它们不会被转换成转义序列的形式
      console.log(`first line
      second line`);
      // first line
      // second line
      console.log(String.raw`first line
      second line`);
      // first line
      // second line
      
      function printRaw(strings) {
      	console.log('Actual characters:');
      	for (const string of strings) {
      		console.log(string);
      	}
      	console.log('Escaped characters;');
      	for (const rawString of strings.raw) {
      		console.log(rawString);
      	}
      }
      printRaw`\u00A9${ 'and' }\n`;
      // Actual characters:
      // ©
      //（换行符）
      // Escaped characters:
      // \u00A9
      // \n
      ```
  
- `"symbol"` 表示值为符号

  - 符号用来创建不会命名冲突的唯一记号，作为对象属性的标识符

  - 使用 `Symbol()` 函数初始化，可以传入一个字符串参数作为对符号的描述

  - 为了避免创建符号包装对象，`Symbol()` 函数不能与 `new` 关键字一起作为构造函数使用（`Boolean`、`String` 或 `Number` 均可；使用符号包装对象可通过`Object()` 函数实现）

  - 全局符号注册表

    - 运行时的不同部分以 `Symbol.for()` 共享和重用符号实例

    - 在全局注册表中定义的符号跟使用 `Symbol()` 定义的符号不等同

    - 必须使用字符串键来创建

      ```javascript
      let emptyGlobalSymbol = Symbol.for();
      console.log(emptyGlobalSymbol); // Symbol(undefined)
      ```

    - `Symbol.keyFor()` 查询全局注册表，接收符号，返回全局符号对应的字符串键；如果查询的不是全局符号，则返回 `undefined`；如果查询的不是符号，则抛出 `TypeError`

  - 使用符号作为属性

    ```javascript
    let s1 = Symbol('foo'),
        s2 = Symbol('bar'),
        s3 = Symbol('baz'),
        s4 = Symbol('qux');
    let o = {
      [s1]: 'foo val'
    };
    // 这样也可以：o[s1] = 'foo val';
    console.log(o);
    // {Symbol(foo): foo val}
    Object.defineProperty(o, s2, {value: 'bar val'});
    console.log(o);
    // {Symbol(foo): foo val, Symbol(bar): bar val}
    Object.defineProperties(o, {
      [s3]: {value: 'baz val'},
      [s4]: {value: 'qux val'}
    });
    console.log(o);
    // {Symbol(foo): foo val, Symbol(bar): bar val,
    // Symbol(baz): baz val, Symbol(qux): qux val}
    ```

    ```javascript
    let s1 = Symbol('foo'),
        s2 = Symbol('bar');
    let o = {
      [s1]: 'foo val',
      [s2]: 'bar val',
      baz: 'baz val',
      qux: 'qux val'
    };
    console.log(Object.getOwnPropertySymbols(o));
    // [Symbol(foo), Symbol(bar)]
    console.log(Object.getOwnPropertyNames(o));
    // ["baz", "qux"]
    console.log(Object.getOwnPropertyDescriptors(o));
    // {baz: {...}, qux: {...}, Symbol(foo): {...}, Symbol(bar): {...}}
    console.log(Reflect.ownKeys(o));
    // ["baz", "qux", Symbol(foo), Symbol(bar)]
    ```

    ```javascript
    // 符号属性是对内存中符号的一个引用，直接创建并用作属性的符号不会丢失
    // 但如果没有显式地保存对这些属性的引用，那么必须遍历对象的所有符号属性才能找到相应的属性键
    let o = {
      [Symbol('foo')]: 'foo val',
      [Symbol('bar')]: 'bar val'
    };
    console.log(o);
    // {Symbol(foo): "foo val", Symbol(bar): "bar val"}
    let barSymbol = Object.getOwnPropertySymbols(o).find((symbol) => symbol.toString().match(/bar/));
    console.log(barSymbol);
    // Symbol(bar)
    ```

  - 常用内置符号（`@@iterator` $\iff$ `Symbol.iterator`）：用于暴露语言内部行为，可以通过重新定义而改变原生结构的行为。如 `for-of` 循环会在相关对象上使用 `Symbol.iterator `属性，就可以通过在自定义对象上重新定义 `Symbol.iterator` 的值，来改变 `for-of` 在迭代该对象时的行为

    - `Symbol.asyncIterator`[ES2018]：表示实现异步迭代器 API 的函数，是一个返回对象供 `for-await-of` 语句使用的默认的 `AsyncIterator` 的方法

      `for-await-of` 循环会利用这个函数执行异步迭代操作。循环时，它们会调用以 `Symbol.asyncIterator` 为键的函数，并期望这个函数会返回一个实现迭代器 API 的对象。很多时候，返回的对象是实现该 API 的 `AsyncGenerator`：

      ```javascript
      class Foo {
        async *[Symbol.asyncIterator]() {}
      }
      let f = new Foo();
      console.log(f[Symbol.asyncIterator]());
      // AsyncGenerator {<suspended>}
      ```

      技术上，这个由 `Symbol.asyncIterator` 函数生成的对象应该通过其 `next()` 方法陆续返回 `Promise` 实例。可以通过显式地调用 `next()` 方法返回，也可以隐式地通过异步生成器函数返回：

      ```javascript
      class Emitter {
        constructor(max) {
          this.max = max;
          this.asyncIdx = 0;
        }
        async *[Symbol.asyncIterator]() {
          while(this.asyncIdx < this.max) {
            yield new Promise((resolve) => resolve(this.asyncIdx++));
          }
        }
      }
      async function asyncCount() {
        let emitter = new Emitter(5);
        for await(const x of emitter) {
          console.log(x);
        }
      }
      asyncCount();
      // 0
      // 1
      // 2
      // 3
      // 4
      ```

      > ❓ 关于异步迭代和 for-await-of 循环的细节，参见附录A。

    - `Symbol.hasInstance`：决定一个构造器对象是否认可一个对象是它的实例的方法，由 `instanceof` 操作符使用以确定一个对象实例的原型链上是否有原型

      ```javascript
      function Foo() {}
      let f = new Foo();
      console.log(Foo[Symbol.hasInstance](f)); // true
      class Bar {}
      let b = new Bar();
      console.log(Bar[Symbol.hasInstance](b)); // true
      
      function Foo() {}
      let f = new Foo();
      console.log(f instanceof Foo); // true
      class Bar {}
      let b = new Bar();
      console.log(b instanceof Bar); // true
      
      // 在继承的类上通过静态方法重新定义这个函数
      class Bar {}
      class Baz extends Bar {
      	static [Symbol.hasInstance]() {
      		return false;
      	}
      }
      let b = new Baz();
      console.log(Bar[Symbol.hasInstance](b)); // true
      console.log(b instanceof Bar); // true
      console.log(Baz[Symbol.hasInstance](b)); // false
      console.log(b instanceof Baz); // false
      ```
    
    -  `Symbol.isConcatSpreadable `：一个布尔值，如果是 `true`，则意味着对象应该用 `Array.prototype.concat()` 打平其数组元素
    
       数组对象默认情况下会被打平到已有的数组，`false` 或假值会导致整个对象被追加到数组末尾；类数组对象默认情况下会被追加到数组末尾，`true` 或真值会导致这个类数组对象被打平到数组实例。其他不是类数组对象的对象在`Symbol.isConcatSpreadable` 被设置为 `true` 的情况下将被忽略。
    
       ```javascript
       let initial = ['foo'];
       let array = ['bar'];
       console.log(array[Symbol.isConcatSpreadable]); // undefined
       console.log(initial.concat(array)); // ['foo', 'bar']
       array[Symbol.isConcatSpreadable] = false;
       console.log(initial.concat(array)); // ['foo', Array(1)]
       
       let arrayLikeObject = { length: 1, 0: 'baz' };
       console.log(arrayLikeObject[Symbol.isConcatSpreadable]); // undefined
       console.log(initial.concat(arrayLikeObject)); // ['foo', {...}]
       arrayLikeObject[Symbol.isConcatSpreadable] = true;
       console.log(initial.concat(arrayLikeObject)); // ['foo', 'baz'] ❓
       
       let otherObject = new Set().add('qux');
       console.log(otherObject[Symbol.isConcatSpreadable]); // undefined
       console.log(initial.concat(otherObject)); // ['foo', Set(1)]
       otherObject[Symbol.isConcatSpreadable] = true;
       console.log(initial.concat(otherObject)); // ['foo']
       ```
    
    -   `Symbol.iterator `：表示实现迭代器 API 的函数，返回对象默认的迭代器供 `for-of` 语句使用
    
       ```javascript
       class Foo {
       	*[Symbol.iterator]() {}
       }
       let f = new Foo();
       console.log(f[Symbol.iterator]());
       // Generator {<suspended>}
       
       class Emitter {
       	constructor(max) {
       		this.max = max;
       		this.idx = 0;
       	}
       	*[Symbol.iterator]() {
       		while(this.idx < this.max) {
       			yield this.idx++;
       		}
       	}
       }
       function count() {
       	let emitter = new Emitter(5);
       	for (const x of emitter) {
       		console.log(x);
       	}
       }
       count();
       // 0
       // 1
       // 2
       // 3
       // 4
       ```
    
    -   `Symbol.match`：用正则表达式去匹配字符串的方法，`String.prototype.match()` 方法使
       用以 `Symbol.match` 为键的函数来对正则表达式求值
    
       ```javascript
       console.log(RegExp.prototype[Symbol.match]);
       // ƒ [Symbol.match]() { [native code] }
       console.log('foobar'.match(/bar/));
       // ["bar", index: 3, input: "foobar", groups: undefined]
       ```
    
       
    
    -  `Symbol.toStringTag `  `Symbol.replace` `Symbol.search` `Symbol.split` `Symbol.toPrimitive ` `Symbol.species`  `Symbol.unscopables `

- `"object"` 表示值为对象（而不是函数）或 `null`

  `null` 值表示一个空对象指针，用于在定义将来要保存对象值的变量时初始化。`undefined` 值由 `null` 值派生而来。

  ```javascript
  console.log(null == undefined); // true
  ```

- `"function"` 表示值为函数（严格来讲函数是一种对象而非数据类型）

<details>
<summary>还没学</summary>

## JavaScript: The Definitive Guide, 7th Edition

## [ES6 入门教程](https://es6.ruanyifeng.com/)

## 你不知道的JavaScript

</details>

## 零零碎碎

- `splice()` 的第一个参数代表从数组中的哪个索引开始移除元素，而第二个参数表示要从数组中的这个位置开始删除多少个元素。 第三个参数可以是一个或多个元素，这些元素会被添加到数组中。

- `reduce()` 方法接收一个函数作为累加器，数组中的每个值（从左到右）开始缩减，最终计算为一个值。**注意:** 对于空数组是不会执行回调函数的。

  ```javascript
  array.reduce(function(total, currentValue, currentIndex, arr), initialValue)
  /*
  total	必需。初始值, 或者计算结束后的返回值。
  currentValue	必需。当前元素
  currentIndex	可选。当前元素的索引
  arr	可选。当前元素所属的数组对象。
  initialValue	可选。传递给函数的初始值
  */
  ```

- `map()` 方法

- `slice()` 方法

- `concat()` 方法

- `filter()` 方法

- `sort()` 方法

- `split()` 方法和 `join()` 方法

- `every()` 方法和 `some()` 方法

- `_` 可忽略当前参数

- 正则表达式

  - 正则表达式 `/bird|cat/`，`/cat/i` 忽略大小写，`/g` 全局多次匹配，`/.un/` 匹配 `*un`，`/[h-s2-6]` 匹配多字母。
  - `/a+/g` 会在 `abc` 中匹配到一个匹配项，并且返回 `["a"]`。 因为 `+` 的存在，它也会在 `aabc` 中匹配到一个匹配项，然后返回 `["aa"]`。如果它是检查字符串 `abab`，它将匹配到两个匹配项并且返回`["a", "a"]`，因为`a`字符不连续，在它们之间有一个`b`字符。 最后，因为在字符串 `bcd` 中没有 `a`，因此找不到匹配项。
  - `*` 匹配出现零次或多次的字符。
  - 正则表达式默认是贪婪匹配，`/t[a-z]*i/` 应用于字符串 `"titanic"` 返回为 `["titani"]`，`/t[a-z]*?i/` 懒惰匹配返回 `["ti"]`。
  - `^` 与 `$` 寻找开头结尾。
  - `\w` 等同于`[A-Za-z0-9_]`，`\W` 相反匹配。
  - `\d` 等同于元字符 `[0-9]`，`\D`等同于字符串 `[^0-9]`。
  - `/\d{n,}/` 至少 `n` 位。
  - `\s` 匹配空格、回车符、制表符、换页符和换行符，类似于元字符 `[ \r\t\f\n\v]`，`\S` 搜寻非空白字符。
  - `?` 前的元素是可选的。
  - 正向先行断言 `(?=...)`中 `...` 是需要存在但不会被匹配的部分，负向先行断言 `(?!...)`，其中 `...` 不存在则返回匹配模式的其余部分。
  - `()` 检查字符组。
  - 捕获组 `/^(\d+)\s\1\s\1$/` 匹配一个只由相同的数字重复三次组成的由空格分隔字符串。
  - `.replace(regex, (string | function))`，可以使用 `$` 访问替换字符串中的捕获组。

- 构造函数 Constructors 函数名首字母大写，使用 `this` 关键字来给它将创建的这个对象设置新的属性

- `prototype` 定义原型属性，可以在所有实例之间共享，可以设置为一个对象但要定义一个 `constructor` 属性；原型链最顶层的 `Object` 定义的 `hasOwnProperty()` 方法只认自身属性；`Object.create(obj)` 创建了一个新对象，并指定了 `obj` 作为新对象的 `prototype`

- 对于不相关的对象，使用 mixin 添加共同行为

- 使属性私有化最简单的方法就是在构造函数中创建变量

- 立即调用函数表达（IIFE）：`(function () {console.log("Chirp, chirp!");} ());`，构造一个函数作用域，防止污染全局变量

- 函数柯里化（Currying）：把接受多个 arity 的函数变换成接受单一 arity 的函数，即重构函数让它接收一个参数，然后返回接收下一个参数的函数，依此类推。是更简短的“偏应用函数（partially applied function）”或“偏函数（partial）”。

  ```javascript
  function unCurried(x, y) {
    return x + y;
  }
  function curried(x) {
    return function(y) {
      return x + y;
    }
  }
  const curried = x => y => x + y
  curried(1)(2)
  
  function impartial(x, y, z) {
    return x + y + z;
  }
  const partialFn = impartial.bind(this, 1, 2);
  partialFn(10); // 13
  ```