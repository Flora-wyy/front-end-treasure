## flex

### 使用
display: flex | inline-flex;
### 决定项目主轴的方向
flex-direction: row | row-reverse | column | column-reverse;   

![flex-direction](https://www.ruanyifeng.com/blogimg/asset/2015/bg2015071005.png)

### 项目一行排不下如何换行 
flex-wrap: normal | wrap | wrap-reverse; 

![normal](https://www.ruanyifeng.com/blogimg/asset/2015/bg2015071007.png)
![wrap](https://www.ruanyifeng.com/blogimg/asset/2015/bg2015071008.jpg)
![wrap-reverse](https://www.ruanyifeng.com/blogimg/asset/2015/bg2015071009.jpg)
### 简写 flex-direction | flex-wrap 
flex-flow: flex-direction | flex-wrap

### 项目在主轴上的对齐方式 
justify-content: flex-start | flex-end | center | space-between | space-around 

![justify-content](https://www.ruanyifeng.com/blogimg/asset/2015/bg2015071010.png)
### 项目在交叉轴上的对齐方式 
align-items: flex-start | flex-end | center | baseline | stretch

![align-items](https://www.ruanyifeng.com/blogimg/asset/2015/bg2015071011.png)
### 多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用 
align-content: flex-start | flex-end | center | baseline | stretch

![align-content](https://www.ruanyifeng.com/blogimg/asset/2015/bg2015071012.png)

### 项目属性

#### order
  项目排序等级，数值越小越在前
#### flex-grow
  项目有足够空间是否拉伸，比例按剩余空间来；0不拉伸
#### flex-shrink
  项目是否压缩，0缩小, 按超出的部分比例来压缩
#### flex-basis
  项目分配空间前占的大小
#### flex
  flex-grow| flex-shrink | flex-basis
  默认 0 1 auto
  none 0 0 auto
  1  1 1 0%
  10% 1 1 10%
#### align-self
  单个项目不一样的排序
  auto | flex-start | flex-end | center | baseline | stretch;

## 参考
[阮一峰 Flex 布局教程](https://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)
