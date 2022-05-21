## manifest 是什么  
当编译器(compiler)开始执行、解析和映射应用程序时，它会保留所有模块的详细要点。这个数据集合称为 "Manifest"，webpack通过manifest来管理模块映射到输出 bundle 的过程

## Runtime 是什么  
webpack 在运行时会注入一块代码用于连接各模块，runtime 包含：在模块交互时，连接模块所需的加载和解析逻辑。包括浏览器中的已加载模块的连接，以及懒加载模块的执行逻辑
  
## 参考资料  
https://www.webpackjs.com/concepts/manifest/  
