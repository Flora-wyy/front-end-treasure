## css
css 模块化一直致力于解决命名冲突，抽象、复用性扩展性等问题


### style in js 
目前主要是react相关项目使用，主要是styled-components、emotion，可以在js使用css，深度与react组件化思想集成，
目前主要是存在性能问题

优点：
在js使用css，让css有了js很强的编码能力，通过js模块化组织相关的模块组件来达到相应的复用性，也不会出现命名冲突
缺点：  
1.运行时问题，需要js动态序列化把这些css插入文档中，增加了性能消耗  
2.包体积变大，加入了相关类库 Emotion 的包体积压缩之后是 7.9k ，而 styled-components 则是 12.7 kB
3.React DevTools调试的时候会更多的嵌套

```typescript
  import styled from "styled-components";


  const Title = <h1 className={css`
        font-size: 1.5em;
        text-align: center;
        color: palevioletred;
    `}></h1>
  ​
  // 创建一个带样式的 h1 标签组件
  const Title = styled.h1`
    font-size: 1.5em;
    text-align: center;
    color: palevioletred;
  `;

  export default function () {
    return <Title></Title>
  }
```

### css modules
导入的模块hash后生产一个唯一的class name解决命名冲突问题，每一个css文件单独存在，需要时候引入从而达成模块化

```typescript
  import styles from './index.scss'
  
  function component() {
    return <div class={styles.container}></div>
  }


```

### 原子化css

原子化css 通过定义了细粒度的类名，解决自定义类名命名的烦恼，让通用的类来实现css类，也能通过@layer 来  
```css
  @layer components {
  .btn-blue {
    @apply bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded;
  }
}

```

@layer utilities
```css
@layer utilities {
  .zzz {
    filter: none;
    color: blue;
  }
  .zzz {
    filter: grayscale(100%);
  }
}
```

或者可以通过插件来扩展原子类
```typescript

// twz.js
import plugin from 'tailwindcss/plugin';

export default plugin(function({ addUtilities }) {
    addUtilities({
        '.z': {
            background: 'blue',
            color: 'yellow'
        },
        '.zz': {
            'font-size': '70px'
        }
    })
})

// 在tailwind.config.js中引入
import twz from './twz.js'
export default {
  content: ["./src/**/*.{html,js,vue}"],
  theme: {
    extend: {},
  },
  plugins: [
    twz
  ],
}

```
