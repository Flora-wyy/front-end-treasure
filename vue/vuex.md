# Vuex
vue状态管理 共享数据抽离  
Vuex注入 init钩子中  
所有子组件的store都是父组件中获取  
Commit通知所有订阅者更新  
通过vue的响应式实例化一个vue对象把state绑定上去  
没有命名空间的时候会触发所有module上的方法  

```typescript
// 声明并注入
import Vue from 'vue'
import Vuex from 'vuex'
Vue.use(Vuex)
const store = new Vuex.Store({
  state: {
    count: 1
  },
  mutations: {
    increment (state) {
      // 变更状态
      state.count++
    }
  },
  getter: {
    doneTodosCount () {
      return this.$store.state.todos.filter(todo => todo.done).length
    }
  },
  actions: {
    increment (context) {
      context.commit('increment')
    }
  }
})
new vue({
  el: "#app"
  store
})
```

### state
当前的
mapState  当映射的计算属性的名称与 state

```typescript
  {
    compute: mapstate({
      // 箭头函数可使代码更简练
      count: state => state.count,

      // 传字符串参数 'count' 等同于 `state => state.count`
      countAlias: 'count',

      // 为了能够使用 `this` 获取局部状态，必须使用常规函数
      countPlusLocalState (state) {
        return state.count + this.localCount
      },
      counts
    })
  }
```

### getter
需要从store派生属性

```typescript
mapGetters
computed: {
  // 使用对象展开运算符将 getter 混入 computed 对象中
    ...mapGetters([
      'doneTodosCount',
      'anotherGetter',
      // ...
    ])
  }
```

### mutations
```typescript
store.commit('increment')
```

### Action
action 用于异步情况
```typescript
store.dispatch('increment')
// mapActions
{
  methods: {
    ...mapActions({
      add: 'increment' // 将 `this.add()` 映射为 `this.$store.dispatch('increment')`
    })
  }
}
```

### Module
由于使用单一状态树，应用的所有状态会集中到一个比较大的对象。当应用变得非常复杂时，store 对象就有可能变得相当臃肿。

为了解决以上问题，Vuex 允许我们将 store 分割成模块（module）。每个模块拥有自己的 state、mutation、action、getter、甚至是嵌套子模块——从上至下进行同样方式的分割：
若要使用拆分的mutation、action、getter需要命名空间
  ```typescript
  const moduleA = {
  state: () => ({ ... }),
  mutations: { ... },
  actions: { ... },
  getters: { ... }
}

const moduleB = {
  state: () => ({ ... }),
  mutations: { ... },
  actions: { ... }
}

const store = new Vuex.Store({
  modules: {
    a: moduleA,
    b: moduleB
  }
})


 modules: {
    account: {
      namespaced: true,
      // 模块内容（module assets）
      state: () => ({ ... }), // 模块内的状态已经是嵌套的了，使用 `namespaced` 属性不会对其产生影响
      getters: {
        isAdmin () { ... } // -> getters['account/isAdmin']
      },
      actions: {
        login () { ... } // -> dispatch('account/login')
      },
      mutations: {
        login () { ... } // -> commit('account/login')
      },
    }
  }
  ```
