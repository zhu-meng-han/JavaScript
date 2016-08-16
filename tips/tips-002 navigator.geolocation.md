
[HTML5 Geolocation](http://www.runoob.com/html/html5-geolocation.html)（地理定位）用于定位用户的位置。

### getCurrentPosition() 方法

> getCurrentPosition() 方法来获得用户的位置。

```js
if (navigator.geolocation) {
  navigator.geolocation.getCurrentPosition( fucnton(position) {
    console.log(position);
  });
} else {
  alert("该浏览器不支持获取地理位置。");
}
```
getCurrentPosition() 方法 - 返回数据

属性                     | 描述
-                       | -
coords.latitude         | 十进制数的纬度
coords.longitude        | 十进制数的经度
coords.accuracy         | 位置精度
coords.altitude         | 海拔，海平面以上以米计
coords.altitudeAccuracy | 位置的海拔精度
coords.heading          | 方向，从正北开始以度计
coords.speed            | 速度，以米/每秒计
timestamp               | 响应的日期/时间

##### 处理错误和拒绝
```js
function showError(error) {
  switch(error.code){
    case error.PERMISSION_DENIED:
      x.innerHTML="用户拒绝对获取地理位置的请求。"
      break;
    case error.POSITION_UNAVAILABLE:
      x.innerHTML="位置信息是不可用的。"
      break;
    case error.TIMEOUT:
      x.innerHTML="请求用户地理位置超时。"
      break;
    case error.UNKNOWN_ERROR:
      x.innerHTML="未知错误。"
      break;
  }
}
```

错误代码：
> * Permission denied - 用户不允许地理定位
> * Position unavailable - 无法获取当前位置
> * Timeout - 操作超时

### watchPosition()- 返回用户的当前位置，并继续返回用户移动时的更新位置

### clearWatch() - 停止 watchPosition() 方法
