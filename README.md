### 档案记录

- 跨域情况下获取文件名 const filename = response.headers.get('Content-Disposition');
  解决方法：后端在响应头 response header 加上 Access-Control-Expose-Headers：Content-Disposition。

- IE8 对 div 添加 click 事件，点击 div 的空白区域无法触发事件，
  解决方法：给 div 的 css 添加 background 属性。

- IE8 对于相邻节点的空白字符会解析为空白节点，如果使用 nextSibling 会取到这个节点。

- IE8/9 浏览器会对 ajax 请求缓存，在 IE8 9 下，进行 Ajax 请求时，若与之前请求相同，则不会再从服务器获取数据，而是直接从本地获取。在使用$.ajax时可以将其cache属性设置为false。
  $.ajaxSetup({ cache: false });

- IE8 对 css 文件的限制
  在 IE8 中，当 css 的规则个数大于 4096 时，它会忽略后面的所有样式。
  IE10 以下的浏览器对 css 有如下限制：
  （1）单个 css 文件的选择器的个数不得大于 4096
  （2）css 文件个数不得大于 31 个
  （3）最多只能嵌入 @import 规则

- IE 的 script 元素只支持 onreadystatechange 事件，不支持 onload 事件。
  FF 的 script 元素不支持 onreadystatechange 事件，只支持 onload 事件。
  参考一下 jquery 的源码：

```
var script = document.createElement("script");

script.src = "xx.js";

script.onload = script.onreadystatechange = function() {
  if (
    !this.readyState || //这是FF的判断语句，因为ff下没有readyState这个值，IE的readyState肯定有值
    this.readyState == "loaded" ||
    this.readyState == "complete" // 这是IE的判断语句
  ) {
    alert("loaded");
  }
};
```

- IE678 window == document为true,document == window竟然为false的神奇特性
- fix ios 设备滑动不流畅问题
  ```
  overflow-y: auto;
  -webkit-overflow-scrolling: touch;
  z-index: 1; /* fix 滑动几次后可滚动区域会卡住的问题*/
  ```
- fix android 手机输入法挡住输入框问题
```
    function androidInputBugFix(){
        // .container 设置了 overflow 属性, 导致 Android 手机下输入框获取焦点时, 输入法挡住输入框的 bug
        // 相关 issue: https://github.com/weui/weui/issues/15
        // 解决方法:
        // 0. .container 去掉 overflow 属性, 但此 demo 下会引发别的问题
        // 1. 参考 http://stackoverflow.com/questions/23757345/android-does-not-correctly-scroll-on-input-focus-if-not-body-element
        //    Android 手机下, input 或 textarea 元素聚焦时, 主动滚一把
        if (/Android/gi.test(navigator.userAgent)) {
            window.addEventListener('resize', function () {
                if (document.activeElement.tagName == 'INPUT' || document.activeElement.tagName == 'TEXTAREA') {
                    window.setTimeout(function () {
                        document.activeElement.scrollIntoViewIfNeeded();
                    }, 0);
                }
            })
        }
 ```
