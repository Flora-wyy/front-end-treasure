### 用法
react声明式 jsx

vue 选项 template模板

### 响应式
vue Object.defineProperty get set, 依赖收集，数据变化自动找到变化的组件修改并渲染
react状态机，状态不可变，setState驱动新的State替换老的State，当数据改变时，以组件为根目录，默认全部重新渲染

### diff
vue的列表比对采用的是首尾指针法，而react采用的是从左到右依次比对的方式，当一个集合只是把最后一个节点移动到了第一个，react会把前面的节点依次移动，而vue只会把最后一个节点移动到最后一个，从这点上来说vue的对比方式更加高效


### 事件
vue 使用的原生事件
react 合成事件