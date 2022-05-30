### 什么是mvc？
mvc 就是model view controller   
model 数据来源，web 服务端数据， 数据库数据
view 数据呈现  
controller 数据到数据呈现之间的转换，即解析数据
通常model 数据变化，就会引起view变化, controller负责解析给view  
所以model就会出现数据监听来通知controller   

### 什么是mvvm? 
mvvm 就是model view ViewModel  
model 数据来源，web 服务端数据， 数据库数据
view 数据呈现 
ViewModel 视图模型层 数据解析, 调用数据渲染视图
MVVM中的持有关系就是：C持有VM，VM持有M   

### 为什么会出现mvvm?
随着现在的数据量越来越大，全部由controller来处理的话就会显得非常臃肿   
Controller被设计出来并不是处理数据解析的。1、管理自己的生命周期；2、处理Controller之间的跳转；3、实现Controller容器   
mvvm是前端的一个模式，让使用者值关心逻辑与数据   
V层和M层的桥梁，而前端框架可以实现这个桥梁，如react、angularJS、vue.js。在这里有个定义：数据绑定  
M层数据的数据变化会影响V层的展示，V层的展示变化也会影响到M层数据的变化，则就是双向数据绑定；
   
M层数据的数据变化会影响V层的展示，V层的展示变化不会影响到M层数据的变化，则就是单向数据绑定。


