Babel 是一个源到源的转换编译器（Transpiler），它的主要作用是将 JavaScript 的高版本语法（例如 ES6）转换成低版本语法（例如 ES5），从而可以适配浏览器的兼容性。

> 温馨提示：如果某种高级语言或者应用语言（例如用于人工智能的计算机设计语言）转换的目标语言不是特定计算机的汇编语言，而是面向另一种高级程序语言（很多研究性的编译器将 C 作为目标语言），那么还需要将目标高级程序语言再进行一次额外的编译才能得到最终的目标程序，这种编译器可称为源到源的转换器。

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c88916e811d348938f248080125a09b0~tplv-k3u1fbpfcp-watermark.awebp)


从上图可知，Babel 的编译过程主要可以分为三个阶段：

- 解析（Parse）：包括词法分析和语法分析。词法分析主要把字符流源代码（Char Stream）转换成令牌流（ Token Stream），语法分析主要是将令牌流转换成抽象语法树（Abstract Syntax Tree，AST）。
- 转换（Transform）：通过 Babel 的插件能力，将高版本语法的 AST 转换成支持低版本语法的 AST。当然在此过程中也可以对 AST 的 Node 节点进行优化操作，比如添加、更新以及移除节点等。
- 生成（Generate）：将 AST 转换成字符串形式的低版本代码，同时也能创建 Source Map 映射。

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/3d2f32124a45465889cf2b9446ec1429~tplv-k3u1fbpfcp-watermark.awebp)

**举个栗子，如果要将 TypeScript 语法转换成 ES5 语法：**

```js
// 源代码
let a: string = 1;
// 目标代码
var a = 1;
```

