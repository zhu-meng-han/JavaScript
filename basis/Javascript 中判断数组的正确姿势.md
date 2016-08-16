### 在 Javascript 中，如何判断一个变量是否是数组？

最好的方式是用 ES5 提供的 Array.isArray() 方法（毕竟原生的才是最屌的）：
```js
var a = [1, 2, 3];
Array.isArray(a); // true
```

但是鉴于低版本 IE 不支持 ES5，如需兼容，需要想想别的办法。

#### typeof ？
我们都知道，数组是特殊的对象，所以数组的 `typeof` 结果也是 `object`，而因为 `null` 的结果也是 `object`，所以如需用 `typeof` 运算符来判断数组，则需要这样写：
```js
var arr = [1, 2, 3];
// object 同时排除 null && 纯对象
typeof arr === 'object' && a !== null && Object.prototype.toString.call(a) !== '[object Object]';
```

#### instanceof ?

来回忆一下 `instanceof` 运算符的使用方式，`a instanceof b`, 如果返回 `true`，表示 `a` 是 `b` 的一个实例。那么如果 `a instanceof Array` 返回 `true`，是不是就说明 `a` 是数组类型呢？`constructor` 是否同样可以判断呢？
```js
var arr = [1, 2, 3];
arr instanceof Array; // true 就是数组？
arr constructor === Array; // true 就是数组？
```

答案是否定的，需要考虑嵌套 `frame` 的情况。

`index.html` 代码：
```html
window.onload = function() {
  var a = window.frames[0].a;
  a instanceof Array; // false
  a constructer === Array; // false
}
```

`a.html` 代码：
```html
window.a = [1, 2, 3];
```

`index.html` 代码中，变量 `a` 确实是一个数组，但是 `a instanceof Array` 的结果却是 `false`。

这是因为每个 `frame` 都有一套自己的执行环境，跨 ｀frame｀实例化的对象彼此不共享原形链。如果 `a instanceof window.frames[0].Array` 则结果就是 `true`

正确的姿势是使用 `Object.prototype.toString()` 进行判断：
```js
var a = [1, 2, 3];
Object.prototype.toString.call(a) === '[object Object]'; // true
```

`Object` 原型链上的 `toString()` 方法大全:
```js
Object.prototype.toString.call(10);  // [object Number]

Object.prototype.toString.call('hello'); //[ object String]

Object.prototype.toString.call(true);  // [object Boolean]

Object.prototype.toString.call([]);  // [object Array]

Object.prototype.toString.call({});   // [object Object]

Object.prototype.toString.call(function() {});    // [object Function]

Object.prototype.toString.call(/a/g);    // [object RegExp]

Object.prototype.toString.call(null);  // [object Null]

Object.prototype.toString.call(undefined);    // [object Undefined]

Object.prototype.toString.call(new Date());  // [object Date]
```

所以 Javascript 中判断数组的函数可以这样写：
```js
function isArray(value) {
  return Array.isArray ? Array.isArray(value) : Object.prototype.toString.call(value) === '[object Array]';
}
```
