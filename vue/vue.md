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

## 概括
1、初始化时，会把data的所有属性通过Object.defineProperty拦截get、set使其observer化，并声明一个订阅者数组dep用于依赖收集。
2、render函数执行的时候，会获取data值，此时会触发getter，然后会把渲染watcher放入dep数组里，完成依赖收集。
3、当data值变化后，会触发setter，通知dep数组里的所有watcher执行update，这里会通过nextTick方法派发到微任务或者宏任务里执行后生成新的Vnode，与old Vnode patch之后再进行DOM更新。

# diff
原理是先同层比较，再比较子节点，重点比较新旧节点都有子节点的情况（核心diff），采用双端比较的算法，同时从新旧节点的两端开始比较。同时借助key值找到可复用节点，再进行相关操作。
具体过程如下：
1、只比较同层新旧节点，判断是否同一节点，如果是就进行PatchVnode，
2、PatchVnode主要逻辑是如果新节点是文本就替换；不是的话，判断是否有有子节点并且不是同一个对象进行updateChildren
3、updateChildren使用了双指针来标记新老节点children索引，然后一一判断，如果是同一节点就再进入PatchVnode递归


# computed 原理
初始化computed 的时候会为每一个计算属性生成一个计算watcher，然后拦截计算属性get set。渲染函数执行时，会获取计算属性值，首次取值因为dirty属性默认为true，这时候触发get根据依赖的data求值。求完值就将dirty值置为false，后续取值只要依赖不发生变化都直接使用缓存。求值时会触发data的get方法，然后会将这个计算watcher推入data对应的dep里面完成依赖收集。后续依赖变化会触发set，然后通知dep的每个watcher更新视图。
# computed 与 watch 区别
1、场景不同：computed是计算属性，适合做值的简单转换；watch是自定义监听器，适合做异步请求和开销较大的操作；
2、computed值会缓存，只要依赖不变，computed值就不会重新计算；
3、watch是如果一个属性变化了就执行一个函数，它有两个选项：
  1、immediate，表示第一次渲染的时候是否要执行这个函数
  2、deep，表示监听一个对象的时候，是否要监听对象的属性变化

<<<<<<< HEAD:vue/vue.md
=======

# watch 原理
watch是vue提供的监听器，用于对data的数据进行监听。非常适用于当数据变化时执行异步或开销比较大的操作。
1、初始化时会对watch对象进行遍历，当对象的属性值为数组时，则遍历数组给数组的每一项创建一个watcher；如果对象属性值不是数组则直接创建watcher。
2、然后watcher初始化的时候，会把监听到的值缓存在watcher.value里，因此会触发对应data中的getter进行依赖收集，就是把当前的user-watcher放入到data对应的dep数组里
3、当data对应值发生变动时，会触发setter，执行dep.notify方法，会通知所有收集的依赖watcher，然后执行watcher的回调，也就是watch中的监听函数。
## deep的作用
当deep为true时，它会⼀层层遍历给对象的所有属性都加上这个监听函数，这样可以检测到对象的每个属性变化，但是这样做会造成更⼤的性能开销。  
优化：可以使⽤字符串监听，即给对象会改变的属性指定该监听器，这样只有遇到该属性才会给其设置监听器，⽽不是给对象的所有属性都加上监听函数。  



>>>>>>> 10bf3bf (feat:更新目录):vue/3.vue.md
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