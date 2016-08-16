## ios上的微信，内嵌H5页面用js无法设置浏览器中的title

* 安卓版正常，Ios内通过 `document.title = 'title'` 不生效

* tips: `document.title` 在js 中 载入时触发，可以生效，当嵌入到Api 请求中时失效

* 解决：

```js
document.title = 'title';
//解决document.title 在 ios 下不生效bug方案 ios内生效
const mobile = navigator.userAgent.toLowerCase();
const length = document.querySelectorAll('iframe').length;
if (/iphone|ipad|ipod/.test(mobile) && !length) {
  const iframe = document.createElement('iframe');
  iframe.style.cssText = 'display: none; width: 0; height: 0;';
  iframe.setAttribute('src', '/favicon.ico');
  iframe.addEventListener('load', () => {
    setTimeout(() => {
      iframe.removeEventListener('load', false);
      document.body.removeChild(iframe);
    }, 0);
  });
  document.body.appendChild(iframe);
}

```
