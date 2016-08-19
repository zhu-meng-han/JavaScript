## JavaScript 字符串常用方法介绍

### `string.repeat(N)` (ES6新增）

* N 参数：number 表示重复的次数

如果传入负数，则报错，传入小数和NaN等同于传入0

```
const a = 'he';

const b = a.repeat(3);

console.log(`${a} --- ${b}`); // he --- hehehe
```

### 是否是字符串

```
typeof 'abc' === 'string' // true
typeof 123 === 'string'   // false
typeof {} === 'string'    // false
```

### `string.indeOf()` - 查询字符串中是否包含指定子字符串。若存在，则返回子字符串在字符串中的下标，否则返回 -1。

```
const str = 'Blue Whale';
str.indexOf('Blue';       // return 0
str.indexOf('Whale');     // return 5
str.indexOf('bluet');     // return -1
str.indexOf('Blue', 0);   // return 0;
```

> `stringObject.indexOf(value,index)`
>  `value` => 规定需检索的字符串值。
>  `index` => 可选的整数参数。规定在字符串中开始检索的位置。它的合法取值是 0 到 stringObject.length - 1。如省略该参数，则将从字符串的首字符开始检索。
> `indexOf()` 对大小写敏感

### `string.length` - 返回数组长度

```
const str = 'abc';
str.length; // return 3
```

### `string.charAt(下标)` - 取字符串中指定下标的字符。如果下标小于0或大于字符串长度，返回空字符。取指定下标的字符也可以用 string[下标]。

```
const str = 'abc';
str.charAt(1)     // return b
str[1]            // return b
str.charAt(4)     // return ''
str.charAt(-1)    // return ''
```

### `string.substring(开始下标, 结束下标)` - 取字符串中指定范围的子字符。

```
const str = 'abcdef';
str.substring(1);     // return 'bcdef'
str.substring(1, 3);  // return 'bc'
str.substring(0, 3);  // return 'abc'
```

### `string.substr(开始下标, 长度)` - 取字符串中指定范围的子字符。

```
const str = 'abcdef';
str.substr(1);    // return 'bcdef'
str.substr(1, 3); // return 'bcd'
str.substr(0, 3); // return 'abc'
```

### 字符串变换

### `string.replace()` - 将字符串中的部分内容替换。

```
const str = 'my name is {name}';
str.replace('{name}', 'menghan.zhu'); // return my  name is menghan.zhu
str; // return my name is {name}
```

### `string.toUpperCase()` - 将字符串变成大写。

```
const str = 'abc';
// 转换成大写
str.replace(/[a~z]/, item => {
  return item.toUpperCase();
}); // return 'Abc'

tr.replace(/[a~z]/g, item => {
  return item.toUpperCase();
}); // return 'ABC'
```
> 同理 `string.toLowerCase()` - 将字符串变成小写。

### `string.trim()` - 去除字符串两头的空格(包括 space, Tab 等)。IE 9+ 支持该方法。

```
const str = '  abc  ';

str.trim();   // return 'abc'
str;          // return '  abc  '

// 对于 IE 8 等老浏览器，可以做以下的兼容。如果用 jQuery ，可以用 $.trim(str)
if (!String.prototype.trim) {
  String.prototype.trim = () => {
    return this.replace(/^[\s\uFEFF\xA0]+|[\s\uFEFF\xA0]+$/g, '');
  }
}
```

### `string.split()` - 将字符串分割成数组

```
const str = 'abc';
str.split(''); // return ['a', 'b', 'c']
const str = 'a&b&c';
str.split('&'); // return ['a', 'b', 'c']
const str = 'a12b233c234d';
str.split(/\d+/); // return ['a', 'b', 'c', 'd']
```
