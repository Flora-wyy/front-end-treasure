### 简介
redux 作为react官方推荐使用的一种状态，并有相关的库

### store 
Store 就是保存数据的地方，你可以把它看成一个容器, 整个应用只能有一个 Store。
```typescript
import { createStore } from 'redux'
const store = createStore(fn)
```

### state 
作为当前的数据状态
```typescript
const state = store.getState();
```

### action
发出一个一个action, 表示状态要发送变更，store.dispatch是唯一发出变更的方式
```typescript
const action = {
  type: 'todo',
  payload: 'data'
}
store.dispatch(action)
```

### reducer
作为处理action时state变化的一个函数, 返回的是一个新的state
```typescript
const reducer = (state, action) => {
  return newState
}
const store = createStore(reducer)
```
### redux 中间件
中间件的概念是在于处理action发出过程中store.dispatch追加的一些处理，通常用于异步操作
```typescript
// 如何使用中间件
import { applyMiddlewares } from 'redux'
const store = createStore(reducer, applyMiddlewares(middleware))
// 如何编写middleware
const middleware = (store) => {
  // 通常对dispatch方法使用装饰器模式
  return (next) => (action) => {
    console.log(`action 触发前打印一波payload: ${action.payload}`);
    next(action)
  }
}

// 异步可以通过redux-thunk 来处理action 是函数的情况
import thunk  from 'redux-thunk'
const store = createStore(reducer, applyMiddlewares(thunk))
function getResponse({dispatch}) {
  fetch().then((json)=>{
    dispatch({
      type: 'data',
      payload: json
    })
  })
}
store.dispatch(getResponse) 

```

### react-redux
函数组件分为UI 和 容器组件，UI为完全依赖Prop没有状态的组件，容器是有自己状态的组件
```typescript
import {connnect, Provide} from 'react-redux'

function Component () {

}

connnect(mapStateToProp, mapDispatchToProp)(Component)

// 使用context来注入到组件中

<Provide store={store}>
  <App />
</Provide>

```





