## 作用
ref转发通常是获取子元素的一种方法。  
通常使用的地方为：
+ 管理焦点，文本选择或媒体播放。
+ 触发强制动画。
+ 集成第三方 DOM 库。
  
## 使用&获取&指向

```typescript
const ref = createRef()
// ref 在元素上ref.current 指向dom元素
<div ref={ref}>

// ref React的class 组件上 ref.current 指向react实例， 
<MyComponent ref={ref}>

// 函数组件通常使用forwardRef来实现转发
const Component = forwardRef((props, ref)=>{
  return <div ref={ref}>
})

// 函数组件内部也使用useRef hooks来实现转发
function Component (props) {
  const ref = useRef()
  return <div ref={ref}>
}

// ref 也支持回调使用
class Component {
  elm = null
  render() {
    return <div ref={(elm)=> this.el = elm}>
  }
}
```


