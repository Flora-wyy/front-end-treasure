### 运行时
Android下是V8引擎
IOS下是jsCore

样式穿透::v-deep

### compile time编译时
定制了一套自己的DSL，在编译打包的过程中，利用 babel 工具通过 AST 进行转译，生成符合小程序规则的代码

### runtime运行时