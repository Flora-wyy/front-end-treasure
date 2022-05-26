## 概念
通过JS对象来描述Dom结构
```typescript
{
  type: 'div',
  props: {
    children: 'text',
    className: 'container'
  }
}

```

## 优点
1.具有跨平台能力，通过这个能力可以在如SSR，Weex，IOS等使用
2.保证patch大量dom更新的性能下限问题

## 缺点
1.无法保证极致性能体验，因为多了一层diff时间和构建