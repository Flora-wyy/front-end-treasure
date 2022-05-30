### 什么是ajax?  
   
Asynchronous JavaScript and XML（异步的 JavaScript 和 XML），是一种用于创建快速动态网页的技术，通过在后台与服务器进行少量数据交换，AJAX 可以使网页实现异步更新。这意味着可以在不重新加载整个网页的情况下，对网页的某部分进行更新  
  
###  什么是XMLHttpRequest？
XMLHttpRequest（XHR）对象用于与服务器交互。通过 XMLHttpRequest 可以在不刷新页面的情况下请求特定 URL，获取数据。这允许网页在不影响用户操作的情况下，更新页面的局部内容。XMLHttpRequest 在 AJAX 编程中被大量使用


### XMLHttpRequest创建ajax实例
  
```javascript  
  
const xmlhttp = new XMLHttpRequest()  
// get method  
xmlhttp.open("GET", "getUserInfo?name=zy&post=123456", true)  
xmlhttp.send()  
// post method  
xmlhttp.open("POST", "getUserInfo", true)  
xmlhttp.setRequestHeader("Content-type","application/x-www-form-urlencoded");  
xmlhttp.send("name=zy&pwd=123456")  

/*** readyState 发送改变回调
  0: 请求未初始化  
  1: 服务器连接已建立  
  2: 请求已接收  
  3: 请求处理中  
  4: 请求已完成，且响应已就绪  
***/
xmlhttp.onreadystatechange = () => {
  if (xmlhttp.readyState === 4 && xmlhttp.status === 200) {
    // todo
  }
}

/** 
 xmlhttp.responseText 字符串类型的响应数据  
 xmlhttp.responseXML xml类型的响应数据  
 mlDoc=xmlhttp.responseXML  
 txt = ""  
 x=xmlDoc.getElementsByTagName("ARTIST")  
 * /
```
### 常用的XMLHttpRequest库  
jquery $.ajax axios

### 什么是fetch?
浏览器原生支持，用于访问和操纵 HTTP 管道的一些具体部分, Fetch 提供了一个更理想的替代方案，可以很容易地被其他技术使用  

### fetch创建的ajax实例
```javascript

fetch('/getUserInfo', {
  method: 'POST',
  body: JSON.stringify({
    name: 'zy',
    pwd: '123456'
  }),
  header: new Headers({
    'Content-Type': 'application/json'
  })
})
  .then(function(response) {
    // 成功回调
    return response.json();
  })
  .catch(function(err) {
    // 失败回调
    console.log(err);
  });

```

### $.ajax与fetch区别
1、fetch采用的是promise，不是回调函数  
2、服务器返回400 500 状态码时并不会reject，只有网络出错导致请求不能完成时，fetch才会被reject  
3、所有版本的 IE 均不支持原生 Fetch  
4、fetch请求默认是不带cookie的，需要设置fetch（URL，{credentials:'include'})  
