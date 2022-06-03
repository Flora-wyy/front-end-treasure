## 乾坤有哪些隔离方式

### legacySandbox
// 不需要遍历window所有的属性
// 同一时间只能激活一个微应用
单实例场景
记录window属性的操作进行还原
addedPropsMapInSandbox 记录新增的变量
modifiedPropsOriginalValueMapInSandbox 更改的变量的原始值
proxy set/get 
set的时候记录修改原对象
用户操作的是proxy对象


### ProxySandbox
多实例场景
// 不需要遍历window所有的属性
只记录不恢复
内部proxy代理对象，
set属性到fakeWindow上
访问fakeWindow, 没有属性从proxy代理到window,



### snapshotSandbox
// 遍历window对象上所有属性性能差
// 同一时间只能激活一个微应用

// 降级
windowSnapshot 记录快照
window 当前window对象
modifyPropsMap 修改对象

active:
  记录当前windon属性，作为快照window
  进入微应用，通过修改项恢复之前的微应用对象
inactive:
  遍历对比当前window 与快照不同，记录修改项
  退出的时候 还原主应用window对象





### 乾坤是怎么创建fakeWindow
```typescript
  // 首先创建一个
  const fakeWindow = {}
  Object.getOwnPropertyNames(window) //获取所有属性
  .filter(()=> {
    const descriptor = Object.getOwnPropertyDescriptor(globalContext, p);
    return !descriptor?.configurable;
  }) // 过滤所有描述对象configurable不为
```