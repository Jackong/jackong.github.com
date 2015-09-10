title: 使用webpack + react开发
date: 2015-09-10 17:06:52
tags: [react, webpack]
category: frontend
---

## 使用.jsx后缀
---

> 让webpack支持各种js后缀

* webpack.config.js
```js
{
    resolve: {
           extensions: ['', '.json', '.node', '.js', '.jsx']
    }
}
```

## 使用ES6语法
---

> npm i --save-dev [babel-loader](http://babeljs.io)

* webpack.config.js
```js
{
    module: {
         loaders: [
             {
                 test: /\.jsx?$/, loader: 'babel', exclude: /(node_modules|bower_components)/,
             }
         ]
    }
}
```

## 使用vendor
---

### 使用vendor的好处
---
* 使用vendor可以把一些公共的module打包到一起，避免重复打包，提交效率
* vendor一般属于非业务module，基本不会修改，可以被缓存，当只有业务代码变动时，避免不必要的请求

### 配置
---

* webpack.config.js
```js
{
    entry: {
        app: './index.jsx',
        vendor: [
            'react',
            'react-router',
            'react-bootstrap',
            'alt'
        ]
    },
    output: {
        filename: '[name]/index.js',
        chunkFilename: '[name]/index.js',
    },
    plugins: [
            new webpack.optimize.CommonsChunkPlugin('vendor', 'vendor/app.js', ['app']),
    ]
}
```

* index.html
```html
<script type="text/javascript" src="./js/vendor/app.js"></script>
<script type="text/javascript" src="./js/app/index.js"></script>
```


## 使用CDN
---

> 除了vendor，我们还可以使用CDN

* webpack.config.js
```js
{
    externals: {//这个配置在编写module时也会被用到，相当于延迟给调用者去加载
        'react': 'React',
        'react-router': 'ReactRouter',
        'react-bootstrap': 'ReactBootstrap',
        'alt': 'Alt'
    }
}
```

* index.html
```html
<script src="//cdn.bootcss.com/react/0.13.3/react.min.js"></script>
<script src="//cdn.bootcss.com/react-router/0.13.3/ReactRouter.min.js"></script>
<script src="//cdn.bootcss.com/react-bootstrap/0.24.5/react-bootstrap.min.js"></script>
<script src="//cdn.bootcss.com/alt/0.17.1/alt.min.js"></script>
```

## 自动实时刷新
---

> npm i --save-dev react-hot-loader

* webpack.config.js
```js
{
    entry: {
        app: './index.jsx',
        vendor: [
            'react',
            'react-router',
            'react-bootstrap',
            'alt'
        ]
    },
    output: {
        path: __dirname + '/public/js/',
        publicPath: '/public/js/',
        filename: '[name]/index.js',
        chunkFilename: '[name]/index.js'
    },
    module: {
         loaders: [
             {
                 test: /\.jsx?$/, loaders: ['react-hot', 'babel'], exclude: /(node_modules|bower_components)/,
             }
         ]
    }
}
```

* server.js
```js
var webpack = require('webpack');
var WebpackDevServer = require('webpack-dev-server');
var config = require('./webpack.config');

const PORT = 3000

new WebpackDevServer(webpack(config), {
  publicPath: config.output.publicPath,
  hot: true,
  historyApiFallback: true
}).listen(PORT, '0.0.0.0', function (err, result) {
  if (err) {
    console.error(err);
    process.exit(1)
  }
  console.log('Listening at 0.0.0.0:' + PORT);
});
```

## Debugger
---
> 这是我的最爱，通过source-map直接对源代码进行debugger，分分钟定位问题

* webpack.config.js
```js
{
    devtool: '#source-map',
    debug: true
}
```
