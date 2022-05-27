# 实例
创建vue实例 init流程
1、initLifecycle   
2、initEvents   
3、initRender   
4、callHook beforeCreate   
5、initInjections   
6、initState    
代理prop和data到vm上   
observe化data 进入响应式流程   
7、initProvide   
8、callHook created   
9、mount挂载组件   

Mixin init state events lifecycle render  
Vue只会维护自己vnode 其他jquery加载的不维护  
State set delete watcher 

# vue响应式流程  
1、数据观察，通过对象上的__ob__属性来确定是否对象已经被观察, data所有属性observe化  
2、observe化监听get上进行依赖收集，即Dep.target上有对象时进行收集, 每个observe的属性都有一个dep对象  
3、每次watcher时都会生成Dep.target, 执行get表达式触发observer上的get进行依赖收集  
mounted时候自动添加一个watcher, 表达式时render函数            
4、每当observe的属性执行set的时候出发该dep里面的依赖更新所有watcher update后 run执行表达式获取新值   
5、观察者没有特殊指定的话将在nexttick更新  

# Vnode
Update触发render获取this._vnode与新渲染的vnode进行对比  
模板解析》ast语法树》ast语法转换render函数字符串》render函数  
update后新老节点进行对比，只对比同层节点，判断当前节点是否是老节点  
对比顺序是从两边向中间对比  

# AST
将代码字符串分割成最小的语法单元数组，  
语法单元  
关键字 标识符 运算符 数字 字符串 空格 注释   

# Vuex
vue状态管理 共享数据抽离  
Vuex注入 init钩子中  
所有子组件的store都是父组件中获取  
Commit通知所有订阅者更新  
通过vue的响应式实例化一个vue对象把state绑定上去  
没有命名空间的时候会触发所有module上的方法  