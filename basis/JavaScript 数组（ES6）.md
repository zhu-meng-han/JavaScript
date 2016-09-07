## JavaScript数组(ES6)

[JavaScript数组](./JavaScript 数组.md)一篇中介绍了ES6之前的数组方法。本篇介绍一下ES6里新增的数组方法:

* `Array.from()`
* `Array.of()`
* `fill()`
* `copyWithin()`
* `find()` `findIndex()`
* `keys()` `values()` `entries()`
* `includes()`
* 数组的空位

#### `Array.from()`

> [].方法名 等价于 Array.prototype.方法

`Array.from()` 方法用于将两类对象转为真正的数组：类似数组的对象、可遍历的对象。

函数声明：`Array.from(arrayLike, [mapFn, [thisArg]]);`

* 第一个参数：`arrayLike` 类数组对象
* 第二个参数：作用类似于数组的map方法，用来对每个元素进行处理，将处理后的值放入返回的数组。

处理arguments对象：

```
// ES5 处理arguments对象：
var args = [].slice.call(arguments);

// ES6 用 from
let args = Array.from(arguments);
```

处理HTMLCollection对象：

```js
// ES5 用forEach 遍历页面所有的div 输出 className
var divs = document.getElementsByTagName('div');
//or
// var tagName = document.querySelectorAll('div');
Array.prototype.forEach.call(divs, function(div) {
    console.log('该div的类名是：' + (div.className || '空') )
});

// ES6用from
Array.from(divs).forEach(div => console.log('该div的类名是：' + div.className || '空'));
```

处理字面量对象：

```js
// ES5
var arrayLike = {
    0: '1',
    1: '2',
    2: '3',
    length: 3
}

Array.prototype.map.call(arrayLike, function (s) {
    return s.toUpperCase();
});
// ['1', '2', '3']

// ES6用from
Array.from(arrayLike, s => s.toUpperCase());
// ['1', '2', '3']
```

上面form用了第二个参数，该语句等价于`Array.from(arrayLike).map(s => s.toUpperCase())`。

处理字符串：

```js
// ES5
Array.prototype.map.call('abc', function(s) {
    return s.toUpperCase()
});
//['A', 'B', 'C']

// ES6
Array.from('abc', s => s.toUpperCase());
//['A', 'B', 'C']
Array.from('zmhan'); // ["z", "m", "h", "a", "n"]
```

对于暂不支持`Array.from()` 方法的浏览器，可以用 `Array.prototype.slice` 方法替换：

```js
const toArray = (() => {
    Array.from ? Array.from : obj => Array.prototype.slice.call(obj);
    // or
    // Array.from ? Array.from : obj => [].slice.call(obj);
})();
```

下面的例子将数组中布尔值为false的成员转为0:

```js
Array.from([1, , 1, 2, , ,0], n => n || 0);
// [1, 0, 1, 2, 0, 0, 0]
```

下面的例子是返回各种数据的类型：

```js
function typesOf () {
  return Array.from(arguments, value => typeof value)
}
typesOf(null, [], 1, 'aaa', NaN, {}, true);
// ["object", "object", "number", "string", "number", "object", "boolean"]
```

#### `Array.of()`

`Array.of()` 将一组值转换为数组。

函数声明： `Array.of(el0, ..., elN)`;

```js
Array(); //[]
Array(3); // [undefined, undefined, undefined]
Array(1, 2, 3); // [1, 2, 3]
```

上面代码中，`Array` 方法没有参数、一个参数、三个参数时，返回结果都不一样。只有当参数个数不少于2个时，Array()才会返回由参数组成的新数组。参数个数只有一个时，实际上是指定数组的长度。

`Array.of()` 的主要目的，就是弥补构造函数 `Array()` 的不足。

`Array.of()` 基本上可以用来替代 `Array()` 或 `new Array()`，并且不存在由于参数不同而导致的重载。它的行为非常统一。

```js
Array.of(); // []
Array.of(3); // [3]
Array.of(1, 2, 3); // [1, 2, 3]
```

`Array.of()` 总是返回参数值组成的数组。如果没有参数，就返回一个空数组。

`Array.of()` 方法可以用下面的代码模拟实现：

```js
function ArrayOf() {
    return [].slice.call(arguments);
}
```

#### `fill()`

`fill()` 用于填充当前数组，返回填充后的数组。

函数声明： `[].fill(value, [start, [end]])`

* value : 填充的元素
* start(可选) : 填充其实位置，默认为0
* end(可选): 填充结束位置，默认到数组尾

```js
var arr = [1, 2, 3];
arr.fill(4); // [4, 4, 4]
arr.fill(4, 1); // [1, 4, 4]
arr.fill(4, 1, 2); // [1, 4, 3]
arr.fill(4, -3, -2); // [4, 2, 3]
```

单个参数时 `fill()` 初始化数组，数组中原有的元素将全被抹去，重新填充新元素。

#### `copyWithin()`

`copyWithin()` 将数组指定位置的元素复制到其他位置（会覆盖原来该位置的元素），最后返回修改后的数组

函数声明： `[].copyWithin(target, [start, [end]])`

* target(必须) : 从该位置开始替换
* start(可选) : 从该位置开始读取数据，默认为0， 如果为负，表示倒着数。
* end(可选) : 到该位置前停止读取数据，默认等于数组长度，如果为负，表示倒着数。

```js
[1, 2, 3, 4, 5, 6].copyWithin(0, 3); // [4, 5, 6, 4, 5, 6]
```

上面的代码表示将从3号位置直到数组结束的成员[4, 5, 6]，复制到从0号开始的位置，即结果覆盖了原来的[1, 2, 3]

```js
// 将3号位复制到0号位
[1, 2, 3, 4, 5, 6].copyWithin(0, 3, 4);
// [4, 2, 3, 4, 5, 6]

[1, 2, 3, 4, 5, 6].copyWithin(0, -2, -1);
// [5, 2, 3, 4, 5, 6]

[1, 2, 3, 4, 5, 6].copyWithin(-2, -3, -1);
// [1, 2, 3, 4, 4, 5]
```

#### `find()`

`find()` 方法，返回第一个满足条件的元素，找不到就返回 `undefined`。

函数声明： `[].find(function(value, index, array) { ... }, [thisArg] );`。

第一个参数是一个回调函数：
* value：遍历的数组内容
* index：对应的索引
* array：数组自身

第二个参数`thisArg`(可选)：改变回调函数里面`this`的指向。


