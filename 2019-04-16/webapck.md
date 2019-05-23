#### webpack按需加载
##### js拆分
###### 前序
a.js
```js
import b from './b.js';
console.log("this is a.js")
const btn = document.querySelector("#btn");
btn.onclick = ()=>{
  b();
}
```
b.js
```js
export default ()=>{
  console.log("this is b");
}
```
webapck.config.js
```js
module.exports = {
  entry:'./a.js',
  output:{
    filename:'[name].js'
  }
}
```
如此打包出来只有一个main.js

###### 拆分
webpack.config.js
```js
module.exports = {
  entry:'./a.js',
  output:{
    filename:'[name].js',
    chunkFilename:'[name].js',// 设置按需加载后的chunk名字,作用就是用来给拆分后的chunk们起名字的配置项
     publicPath:'dist/' // 设置基础路径
  }
}
```
a.js
```js
// import b from './b.js';
console.log("this is a.js")
const btn = document.querySelector("#btn");
btn.onclick = ()=>{
    import(/* webpackChunkName: "b" */ './b').then(function(module){
      const b = module.default;
      b();
    })
}
```
#### webpack热更新
##### 前序
###### 集成webpack-dev-server
```js
{
  "devDependencies": {
    "webpack-dev-server": "^3.1.9"
  },
  "scripts": {
    "start:dev": "webpack-dev-server"
  },
  "dependencies": {
    "webpack": "^4.20.2",
    "webpack-cli": "^3.1.2"
  }
}
```
###### 修改webpack.config.js
```js
var path = require('path');
module.exports = {
  entry:'./a.js',
  mode:'development',
  output:{
    filename:'[name].js',
    chunkFilename:'[name].js',// 设置按需加载后的chunk名字
    publicPath:'dist/'
  },
  devServer: {
    contentBase: './',
    compress: true,
    port: 9000
  }
}

```
这一次不再通过webpack命令来执行了
而是通过npm run start:dev命令行来执行
webpack-dev-server会读取webpack.config.js中的devServer配置
ok，devServer已经集成好了
##### 启动
###### 修改webpack.config.js
```js
var path = require('path');
var webpack = require('webpack');
module.exports = {
  entry:'./a.js',
  mode:'development',
  output:{
    filename:'[name].js',
    chunkFilename:'[name].js',// 设置按需加载后的chunk名字
    publicPath:'/dist/'//????
  },
  devServer: {
    contentBase: './',
    compress: true,
    port: 9000,
    hot: true, // 开启热更新
  },
  plugins: [ // 开始热更新
      new webpack.NamedModulesPlugin(),
      new webpack.HotModuleReplacementPlugin()
  ],
}
```
上面一共起作用的就是3句话：
devServer中的hot语句
plugins中的两个webpack内置插件 将这两个插件开启后，还不行，还需要修改入口文件
```js
// import b from './b.js';
console.log("this is a.js")
const btn = document.querySelector("#btn");
btn.onclick = ()=>{
  import(/* webpackChunkName: "b" */ './b').then(function(module){
    const b = module.default;
    b();
  })
}

if (module.hot) {// 开启热替换
     module.hot.accept()
}

```