title: react进阶式教程
date: 2015-11-24 10:11:01
tags: [react, gulp, webpack]
categories: frontend
thumbnailImage: http://7xkwtq.com1.z0.glb.clouddn.com/reactjs.png
---

基本环境搭建

<!-- more -->

# react
---
react现在越来越流程起来了，看到很多公司已经开始在做各种相关的技术分享与实践。
为了使新接触react的同事更好的入门，形成技术氛围，推动项目应用与发展。
故决定写下react进阶式的教程，希望对新手有所帮助。

# package.json
```js
{
    //...
    "dependencies": {
      "react": "^0.14.2",
      "react-dom": "^0.14.2" //用于render
    },
    "devDependencies": {
      "babel-core": "^6.1.21",
      "babel-loader": "^6.2.0", //用于webpack loader
      "babel-preset-es2015": "^6.1.18", //用于支持es6大部分语法与编译
      "babel-preset-react": "^6.1.18", //用于支持react语法与编译
      "gulp": "^3.9.0", //用于管理项目构建
      "webpack-stream": "^2.1.1" //用于在gulp中使用webpack
    }
    //...
}
```

# webpack
---
```js
const webpack = require('webpack')
const path = require('path')

module.exports = {
  entry: {
    app: './public/js/index.jsx',//定义要编译的入口文件
    vendor: [//定义公用模块，将业务逻辑与公用模块分开打包，有得于不常改变的vendor作缓存
      'react'
    ]
  },
  output: {
    path: path.join(__dirname, 'public/js/'),
    filename: '[name]/index.js',
    chunkFilename: '[name]/index.js',
  },
  plugins: [
     //在app中抽出vendor中定义的模块打包到vendor/app.js
    new webpack.optimize.CommonsChunkPlugin('vendor', 'vendor/app.js', ['app']),
  ],
  resolve: {
      //让webpack可以处理各种后缀
    extensions: ['', '.json', '.node', '.js', '.jsx']
  },
  module: {
    loaders: [{//使用babel-loader对.jsx进行解析编译
      test: /\.jsx?$/,
      loader: 'babel',
      exclude: /(node_modules|bower_components)/,
    }]
  }
}
```

# gulp
---
```js
const gulp = require('gulp')
const webpack = require('webpack-stream')
const config = require('./webpack.config')

//对./public/js/index.jsx进行webpack编译
gulp.task('webpack', () => {
    return gulp.src('./public/js/index.jsx')
        .pipe(webpack(config))
        .pipe(gulp.dest('./public/js/'))
})

//监听public/js/下所有.jsx文件变化，并执行webpack任务
gulp.task('watch', ['webpack'], () => {
     gulp.watch('./public/js/**/*.jsx', ['webpack'])
})
```

# index.html
---
```html
<!DOCTYPE html>
<html lang="zh-CN">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <meta author="jackong">
    <title>react tutorial</title>
    <!-- 引入公用模块 -->
    <script src="js/vendor/app.js"></script>
  </head>
  <body>
        <!-- App渲染节点 -->
      <div id="app"></div>
      <!-- 引入业务模块，放到body最后，免去DOMContentLoaded事件 -->
      <script src="js/app/index.js"></script>
  </body>
</html>
```

# index.jsx
---
```js
import React from 'react'
import {render} from 'react-dom'

import App from './components/app'

try {
    //将App组件render到app节点
    render(<App name='tutorial' />, document.getElementById('app'))
} catch(err) {
    console.error(err)
}
```

# components/app.jsx
---
```js
import React, { PropTypes } from 'react'

class App extends React.Component {
    static propTypes = {
        //对name进行校验
        name: PropTypes.string.isRequired
    }
    render () {
        return (
            <div>
                {this.props.name}
            </div>
        )
    }
}

export default App
```

# 章结
> 到此为止，一个`Hello World`级别的react app就这样完成了。
下一章节将引入state, ref, css-in-js概念，敬请期待。
