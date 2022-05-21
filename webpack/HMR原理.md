## HMR是什么  
HMR（模块热更新）是运行应用程序在运行中进行更新时无需重新加载页面的一种技术。

## HMR作用  
保留在完全重新加载页面时丢失的应用程序状态。  
只更新变更内容，以节省宝贵的开发时间。  
调整样式更加快速 - 几乎相当于在浏览器调试器中更改样式。  

## HMR怎么实现的  
更新请求发起流程
### 在应用程序中
通常是监听到文件变化  
应用程序代码要求 HMR runtime 检查更新。  
HMR runtime（异步）下载更新，然后通知应用程序代码。  
应用程序代码要求 HMR runtime 应用更新。  
HMR runtime（同步）应用更新。  

### 在编译器中  
更新manifast  
更新发生变更的chunk  

### 在模块中  
通常是各种loader已经集成HMR API实现更新补丁

### 参考资料
https://baijiahao.baidu.com/s?id=1710928200156345206&wfr=spider&for=pc  
https://www.webpackjs.com/concepts/hot-module-replacement/
