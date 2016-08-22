## JavaScript 数组常用方法介绍

* `array.pop()` - 删除数组最后一位元素。

```js
var arr = [1, 2, 3];
arr.pop();    // return 3
arr;          // return [1, 2]
```

* `array.shift()` - 删除数组第一位元素。

```js
var arr = [1, 2, 3];
arr.shift();  // return 1
arr;          // return [2, 3]
```

* `array.push()` - 往数组的末尾新增一个或多个元素。

```js
var arr = [];
arr.push(1);    // return arr.length 1
arr;            // return [1]
```

* `array.unshift()` - 往数组的开头新增一个或多个元素。

```js
var arr = [1, 2, 3, 4];
arr.unshift(0);   // return arr.length 5
arr;              // return [0, 1, 2, 3, 4]
```

* `array.reverse()` - 把数组元素顺序逆转。

```js
var arr = [1, 3, 2];
arr.reverse();        // return [2, 3, 1]
```

* `array.sort()` - 数组排序。

```js
var arr = [1, -2, -1, 0, 2];
arr.sort();    // return [-1, -2, 0, 1, 2]
arr.sort((a, b) => a > b ? 1 : -1);
// return [-2, -1, 0, 1, 2]
```

* `array.splice()` - 给数组添加或者删除元素。splice(开始下标, 删除个数，插入元素(可以多个)）

```js
var arr = [1, 2, 3, 4];
arr.splice(1, 2); // return [2, 3]
arr;              // return [1, 2]
arr = [1, 2, 3, 4];
arr.splice(1, 2, 'a', 'b', 'c');  // return [2, 3]
arr;   // return [1, "a", "b", "c", 4]
```

##### 注意：当数组执行上面的这些方法时，都会修改原数组。

## 迭代方法

* `array.forEach()` - 遍历数组。

```js
var arr = [a, b, c];
arr.forEach((value, index) =>  console.log(index, value));
/* return
0 "a"
1 "b"
2 "c"
*/
```

* `array.filter()` - 从数组中找出所有符合指定条件的元素

```js
var arr = [2, 4, -3, 0];
arr.filter(value => value > 0);
// return [2, 4]
```

* `array.every()` - 数组中是否每个元素都满足指定的条件。

```js
var arr = [1, 4, 50, 23];
arr.every(value => value > 10);
// return false
[1, 2, 3, 5].every(value => value > 0);
// return true
```

* `array.some()`- 数组中是否有元素满足指定的条件。

```js
var isSomePositive = [1,3, -2, 4].some(value => value > 0);
// return true
isSomePositive = [-1, -3].some(value => value > 0);
// return false
```

* `array.map()` - 将数组映射成另一个数组。

```js
[1, 2, 3, 4].map(value => value * value);
// return [1, 4, 9, 16]
```

* `array.reduce()` - 将数组合成一个值。

```js
[1, 2, 3].reduce((pre, value) => pre + value);
// return 6
```

## 其他方法

*  `Array.isArray()` - 是否是数组。IE9+ 支持该方法。

```js
Array.isArray(3);   // return false
Array.isArray({});  // return false
Array.isArray([]);  // return true
```

* `array.concat()` - 合并数组或合并数组的值。

```js
[1, 2, 3].concat(4, 5);   // return [1, 2, 3, 4, 5]
```

* `array.join()` - 合并数组所有元素拼接成字符串。

```js
[1, 2, 3].join();     // return '1,2,3'
[1, 2, 3].join('');     // return '123'
[1, 2, 3].join('@')   // return '1@2@3'
```

* `array.slice()` - 选择数组中的一部分元素。

> slice(开始下标, 结束下标（可选，默认为数组长度）)

```js
['a', 'b', 'c', 'd'].slice(1);  //return ["b", "c", "d"]
['a', 'b', 'c', 'd'].slice(1,2);  //return ["b"]
['a', 'b', 'c', 'd'].slice(1,3);  //return ["b", "c"]
```

* `array.indexOf()` - 查找数组中指定元素的下标。

```js
['a', 'b', 'c', 'd'].indexOf('c');  //return 2
'a', 'b', 'c', 'd'].indexOf('e');  //return -1
```

* `array.lastIndexOf()` - 查找数组中指定元素的下标。查找方向为从后往前

```js
['a', 'b', 'c', 'd'].lastIndexOf('c'); // return 2
['a', 'b', 'c', 'd'].lastIndexOf('f'); // return 2=-1
```
