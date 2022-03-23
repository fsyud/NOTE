在Webpack运行的生命周期中会广播出许多事件，Plugin可以监听这些事件，在合适的时机通过Webpack提供的API改变输出结果。通俗来说：一盘美味的盐豆炒鸡蛋需要经历烧油 炒制 调味到最后的装盘等过程，而plugin相当于可以监控每个环节并进行操作，比如可以写一个少放胡椒粉plugin,监控webpack暴露出的生命周期事件(调味)，在调味的时候执行少放胡椒粉操作。那么它与loader的区别是什么呢？上面我们也提到了loader的单一原则,loader只能一件事，比如说less-loader,只能解析less文件，plugin则是针对整个流程执行广泛的任务。

一个基本的plugin插件结构如下

```js
class firstPlugin {
  constructor (options) {
    console.log('firstPlugin options', options)
  }
  apply (compiler) {
    compiler.plugin('done', compilation => {
      console.log('firstPlugin')
    ))
  }
}
module.exports = firstPlugin
```

> compiler 、compilation是什么？

- compiler 对象包含了 Webpack 环境所有的的配置信息。这个对象在启动 webpack 时被一次性建立，并配置好所有可操作的设置，包括 options，loader 和 plugin。当在 webpack 环境中应用一个插件时，插件将收到此 compiler 对象的引用。可以使用它来访问 webpack 的主环境。
- compilation对象包含了当前的模块资源、编译生成资源、变化的文件等。当运行webpack 开发环境中间件时，每当检测到一个文件变化，就会创建一个新的 compilation，从而生成一组新的编译资源。compilation 对象也提供了很多关键时机的回调，以供插件做自定义处理时选择使用。


> compiler和 compilation的区别在于

- compiler代表了整个webpack从启动到关闭的生命周期，而compilation只是代表了一次新的编译过程
- compiler和compilation暴露出许多钩子，我们可以根据实际需求的场景进行自定义处理

下面我们手动开发一个简单的需求,在生成打包文件之前自动生成一个关于打包出文件的大小信息

新建一个webpack-firstPlugin.js

```js
class firstPlugin{
  constructor(options){
    this.options = options
  }
  apply(compiler){
    compiler.plugin('emit',(compilation,callback)=>{
      let str = ''
      for (let filename in compilation.assets){
        str += `文件:${filename}  大小${compilation.assets[filename]['size']()}\n`
      }
      // 通过compilation.assets可以获取打包后静态资源信息，同样也可以写入资源
      compilation.assets['fileSize.md'] = {
        source:function(){
          return str
        },
        size:function(){
          return str.length
        }
      }
      callback()
    })
  }
}
module.exports = firstPlugin 
```

如何使用

```js
const path = require('path')
const firstPlugin = require('webpack-firstPlugin.js')
module.exports = {
    // 省略其他代码
    plugins:[
        new firstPlugin()
    ]
}
```
执行npm run build即可看到在dist文件夹中生成了一个包含打包文件信息的fileSize.md
![image](https://user-images.githubusercontent.com/26371465/159724748-e7f0f445-81a4-4899-a887-c5ffbc21f40f.png)

![image](https://user-images.githubusercontent.com/26371465/159724880-ad55c845-659a-4d98-b738-b8e159f240d6.png)



