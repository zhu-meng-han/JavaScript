### 删除数组内不想要的数据

```js
function removeIf(array, callback) {
  const result = [];
  for (let i = 0; i < array.length;) {
    if (callback(array[i], i)) {
      result.push(...array.splice(i, 1));
    } else {
      ++i;
    }
  }
  return result;
}

const orders = {
  '1469116800000': [
    {
      'id': 2347029,
      'count': 1,
      'timestamp': 1469008985973
    },
    {
      'id': 2347030,
      'count': 1,
      'timestamp': 1469008985973
    }
  ],
  '1469376000000': [
    {
      'id': 2347031,
      'count': 1,
      'timestamp': 1469008987056
    }
  ],
  '1469462400000': [
    {
      'id': 2347032,
      'count': 1,
      'timestamp': 1469008990389
    },
    {
      'id': 2347033,
      'count': 1,
      'timestamp': 1469008990389
    }
  ]
};
const idList = [2347030, 2347031, 2347032];

// 第一种遍历对象方法
for (const i in orders) {
  if (orders.hasOwnProperty(i)) {
    removeIf(orders[i], x => ~idList.indexOf(x.id));
  }
}

// 第二种遍历对象方法
Object.keys(orders).map(key => {
  removeIf(orders[key], x => ~idList.indexOf(x.id));
});
```
