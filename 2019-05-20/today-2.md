在实践中通过判断 userAgent 来决定使用哪种方法：
```js
const ua = window.navigator.userAgent.toLocaleLowerCase();
const isIOS = /iphone|ipad|ipod/.test(ua);
const isAndroid = /android/.test(ua);
```
##### 优化OPTIONS请求：Access-Control-Max-Age 或者 避免触发
可见一旦达到触发条件，跨域请求便会一直发送2次请求，这样增加的请求数是否可优化呢？答案是可以，OPTIONS预检请求的结果可以被缓存。

Access-Control-Max-Age这个响应首部表示 preflight request  （预检请求）的返回结果（即 Access-Control-Allow-Methods 和Access-Control-Allow-Headers 提供的信息） 可以被缓存的最长时间，单位是秒。(MDN)

如果值为 -1，则表示禁用缓存，每一次请求都需要提供预检请求，即用OPTIONS请求进行检测。
评论区的朋友提醒了，尽量避免不要触发OPTIONS请求，上面例子中把content-type改掉是可以的。在其他场景，比如跨域并且业务有自定义请求头的话就很难避免了。现在使用的axios或者superagent等第三方ajax插件，如果出现CORS预检请求，可以看看默认配置或者二次封装是否规范。
##### 总结
OPTIONS请求即预检请求，可用于检测服务器允许的http方法。当发起跨域请求时，由于安全原因，触发一定条件时浏览器会在正式请求之前自动先发起OPTIONS请求，即CORS预检请求，服务器若接受该跨域请求，浏览器才继续发起正式请求。


##### 数组排序
```js
array.sort(function(a,b){
    return a-b
})
```
##### 获取数组中的最大值和最小值
```js
var  numbers = [5, 458 , 120 , -215 , 228 , 400 , 122205, -85411]; 
var maxInNumbers = Math.max.apply(Math, numbers); 
var minInNumbers = Math.min.apply(Math, numbers);
//清空数组
var myArray = [12 , 222 , 1000 ];  
myArray.length = 0; 
```