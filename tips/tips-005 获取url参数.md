### 获取url参数

```js
function getParam(name) {
  const reg = new RegExp('(^|&)' + name + '=([^&]*)(&|$)');
  const r = window.location.search.substr(1).match(reg);
  return r !== null ? decodeURIComponent(r[2]) : null;
}

// 假定url为：http://ele.me?date=20160816&id=3214321234;

var date = getParam(date);
id = getParam(id);
```
