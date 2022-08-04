### 简介
react 框架内部的运作可以分为 3 层：
Virtual DOM 层，描述页面长什么样。
Reconciler 层，负责调用组件生命周期方法，进行 Diff 运算等。
Renderer 层，根据不同的平台，渲染出相应的页面，比较常见的是 ReactDOM 和 ReactNative。


在 Fiber 诞生之前，React 处理一次 setState()（首次渲染）时会有两个阶段：
调度阶段（Reconciler）：这个阶段React用新数据生成新的 Virtual DOM，遍历 Virtual DOM，然后通过 Diff 算法，快速找出需要更新的元素，放到更新队列中去。这个过程可能会被打断
渲染阶段（Renderer）：这个阶段 React 根据所在的渲染环境，遍历更新队列，将对应元素更新。在浏览器中，就是更新对应的 DOM 元素。这个阶段不能被打断

如果多个dom更新的情况下，整个会堵塞其他流程工作，为了解决这个问题，react推出了Fiber，它能够将渲染工作分割成块并将其分散到多个帧中。同时加入了在新更新进入时暂停，中止或重复工作的能力和为不同类型的更新分配优先级的能力


分片更新
requestAnimationFrame 处理优先级高的任务如用户输入，
使用requestIdleCallback实现

如果优先级高于待处理的工作，或者没有 截止日期 或者截止日期尚未到达，Fiber 可以在一帧之后安排多个工作单元。而下一组工作单元会被带到更多的帧上。这就是使 Fiber 有可能暂停、重用和中止工作单元的原因。

对于前者，暂停/重启意味着我们需要保存状态，这里在实现上用到了具有链表和指针的“单链表树遍历算法”，能够记录遍历过程中的上一步和下一步。。Fiber采用的链表包含3个指针，return指向父Fiber节点，child指向大儿子Fiber节点，sibling指向兄弟Fiber节点。一个Fiber节点对应一个任务节点。

为了达到这种效果，就需要有一个调度器 (Scheduler) 来进行任务分配。任务的优先级有六种：

synchronous，与之前的操作一样，同步执行
task，在next tick之前执行
animation，下一帧之前执行
high，在不久的将来立即执行
low，稍微延迟执行也没关系
offscreen，下一次render时或scroll时才执行

由于 reconciliation 的阶段会被打断，可能会导致 commit 前的这些生命周期函数多次执行。react 官方目前已经把 componentWillMount、componentWillReceiveProps 和 componetWillUpdate 标记为 unsafe，并使用新的生命周期函数 getDerivedStateFromProps 和 getSnapshotBeforeUpdate 进行替换。


workLoop中拿出一个任务，每执行完一个‘执行单元‘，就检查一下剩余时间是否充足，如果充足就进行执行下一个执行单元，反之则停止执行，保存现场，等下一次有执行权时恢复:


## fiber
Fiber 包含的属性可以划分为 5 个部分:
组成|内容
--|--
结构信息| 这个上文我们已经见过了，Fiber 使用链表的形式来表示节点在树中的定位
节点类型信息 | 这个也容易理解，tag表示节点的分类、type 保存具体的类型值，如div、MyComp
节点的状态 |节点的组件实例、props、state等，它们将影响组件的输出
副作用 |这个也是新东西. 在 Reconciliation 过程中发现的'副作用'(变更需求)就保存在节点的effectTag 中(想象为打上一个标记).那么怎么将本次渲染的所有节点副作用都收集起来呢？ 这里也使用了链表结构，在遍历过程中React会将所有有‘副作用’的节点都通过nextEffect连接起来
替身 | React 在 Reconciliation 过程中会构建一颗新的树(官方称为workInProgress tree，WIP树)，可以认为是一颗表示当前工作进度的树。还有一颗表示已渲染界面的旧树，React就是一边和旧树比对，一边构建WIP树的。 alternate 指向旧树的同等节点。


### fiber 如何对比

## 双缓冲
WIP 树构建这种技术类似于图形化领域的'双缓存(Double Buffering)'技术, 图形绘制引擎一般会使用双缓冲技术，先将图片绘制到一个缓冲区，再一次性传递给屏幕进行显示，这样可以防止屏幕抖动，优化渲染性能。
放到React 中，WIP树就是一个缓冲，它在Reconciliation 完毕后一次性提交给浏览器进行渲染。它可以减少内存分配和垃圾回收，WIP 的节点不完全是新的，比如某颗子树不需要变动，React会克隆复用旧树中的子树。
双缓存技术还有另外一个重要的场景就是异常的处理，比如当一个节点抛出异常，仍然可以继续沿用旧树的节点，避免整棵树挂掉。

[参考 https://juejin.cn/post/6844903975112671239#heading-1](https://juejin.cn/post/6844903975112671239#heading-1)