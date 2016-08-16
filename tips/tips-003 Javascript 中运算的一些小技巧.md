## 运算符中的一些小技巧

* `%` 运算符

> 取余运算符运算结果的正负号由第一个运算子的正负号决定

```js
-1 % 2 // return -1
1 % -2 // return 1
```
取余时，当数据为负数时会报错
```js
// bad
function isOdd(n) {
  return n % 2 === 1;
}
isOdd(-5);  // return false
isOdd(-4);  // return false

// good
function isOdd(n) {
  return Math.abs(n % 2) === 1;
}
isOdd(-5); // return true;
isOdd(-4); return false
```

* `+` 运算符

> `+` 运算符与其他运算符不太一样，我们知道它可以用来连接字符串操作，是因为用+运算符的时候它通常会将其他类型的值转为字符串，但是除了它比如说-运算符等都会将其他类型的值转换为数值，像这样：

```js
const str = new Date();
typeof (str + 1); return 'string'
typeof (str - 1); return 'number'
```
> 当 `+` 运算符作为数值运算符放在其他值前面的时候，可以用于将任何值转为数值，就像Number函数那样:

```js
const str = new Date();
typeof +str; // return 'number'
+true;       // return 1
+[];         // return 0
+{};         // reutn NaN
```

*  `!`取反运算符

> `！` 取反运算符连续对同一个值进行取反运算等于将其转换为对应的布尔值，就像Boolean函数那样:

```js
!!x;
// 等同于
Boolean(x);
```

此外，如果我们想排除null这个对象，可以这样写:

```js
if (!!x) {
  //do something
}
```

> 这是因为:!!null 值是 false，其他的 object !!obj 值都是 true。


此外，`void` 运算符的作用是用来执行一个表达式，然后返回undefined

```js
void 0 // return  'undefined'
```
