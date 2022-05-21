### PubilcPath
该配置会让所有引入资源的路径上新加上该路径，  
用法  
运行时中使用变量__webpack_public_path__可以动态改变，可以在一些需要运行时才能判断的情况下使用，比如，为浏览器准备两份代码ES6和ES5，支持ES6的需要定位到另一个CDN地址上；
通常该使用配置默认。  
即引用的是相对路径如HTML 中 <script src='index.js'></script>引用的是index.html同目录下的index.js，若index.js打包后由cdn提供或者不再这个路径下，则要改变这个配置
该配置会改变所有静态资源引用前缀，若目录是树状结构的明显一个publicPath就不够用了

需要结合一些插件的PublicPath来做到定制

chunk 和 bundle区别？
 https://webpack.docschina.org/glossary
chunk 构建过程中的代码，属于中间产物
chunk 有两种形式：
● initial(初始化) 是入口起点的 main chunk。此 chunk 包含为入口起点指定的所有模块及其依赖项。
● non-initial 是可以延迟加载的块。可能会出现在使用 动态导入(dynamic imports) 或者 SplitChunksPlugin 时。
bundle 是处理后最终生成的dist 文件产物，属于最终产物
有哪些常用的魔法注释？
     https://webpack.docschina.org/api/module-methods/#magic-comments
      /*  webpackChunkName  */  chunkname 设置  优先级 splitChunk > webpackChunkName > ChunkFileName

     https://webpack.docschina.org/guides/code-splitting/#prefetchingpreloading-modules
      /*  webpackPrefetch  */ 预拉取  空闲时间加载按需加载文件， 
      /*  webpackPreLoad  */ 预加载   并行下载，后续执行
     使用的是HTML5 <link rel="prefetch/ preload" href=' ...' />
ChunkFileName 
    string or function
   哪些文件会受此选项影响？
官方解释此选项决定了非初始（non-initial）chunk 文件的名称，即非entry 入口文件，理解import 
   [name].js 占位符name 取的是什么？

分别指定和不指定运行时chunkName，接着打断点观察下：
import('.later') 没有chunkName null，并不是按导入文件名来进行的设置为later

而指定了最终

Tree Shaking
index       utils
怎么开启？
    mode production 自动开启；
    手动开启需要 usedExports 标记无引用代码 ， minimize 压缩去掉无引用代码
    usedExports 用于标记模块是否被引用，并不导出未使用的成员
   usedExports 只能标记顶层的import/export
usedExports : true  , minimize: false

usedExports : true  , minimize: true
usedExports : false  , minimize: false

usedExports : false  , minimize: true

sideEffects
  mode production 自动开启；手动开启sideEffects：true
  开启后webpack会去识别包中package.json 中的sideEffects字段
   新增引入包中无sideEffects
  
包含副作用

无sideEffects
