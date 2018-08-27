---
title: 基于 webpack4 搭建 一个简单 的 React 脚手架 （二）
date: 2018-08-27 16:36:01
tags:
    - React
    - webpack
cover: https://www.pexels.com/photo/person-holding-black-android-smartphone-861126/
---

  上一篇文章我们已经基本实现了一个简单的框架， 现在， 我们继续把我们的项目完善一下~

  [上一篇：基于 webpack4 搭建 一个简单 的 React 脚手架 （一）][1]

  [webpack4 官方文档 ，请戳这里~][2]


## 生产环境构建
   
   开发环境(development)和生产环境(production)的构建目标差异很大, 所以我们在使用时通常会为每个环境编写一个独立的配置文件。为了出现大量的重复代码， 我们可以提取一个公共的配置文件， 通过  webpack-merge 可以把webpack合并起来。

   webpack-merge 安装

     yarn add webpack-merge -D

   最终， 我们的 代码结构如下：
```
dist
src
.babelrc
package.json
webpack
├── webpack.common.js
├── webpack.dev.js
└── webpack.prod.js
```


   webpack.common.js:

```
const path = require('path');
const CleanWebpackPlugin = require('clean-webpack-plugin');
const HtmlWebpackPlugin = require('html-webpack-plugin');
module.exports = {
entry: {
    app: './src/index.js'
},
module: {
    rules: [
        {
            test: /\.js$/,
            exclude: /node_modules/,
            use: {
                loader: "babel-loader"
            }
        }
    ]
},
plugins: [
    new CleanWebpackPlugin(['dist']),
    new HtmlWebpackPlugin({
        template: "./src/index.html",
        filename: "index.html"
    }),
],
output: {
    filename: '[name].bundle.js',
    path: path.resolve(__dirname, '../dist')
}
};
```

   webpack.dev.js

```
const path = require('path');
const webpack = require('webpack');
const merge = require('webpack-merge');
const common = require('./webpack.common.js');

module.exports = merge(common, {
  mode: 'development',
  devtool: 'inline-source-map',
  devServer:{
    contentBase:path.join(__dirname,"dist"),
    compress: true,
    port: 8033,
    hot: true,
  },
  plugins: [
    new webpack.HotModuleReplacementPlugin()
  ],
});
```

   webpack.prod.js


```
const merge = require('webpack-merge');
const common = require('./webpack.common.js');

module.exports = merge(common, {
  mode: 'production',
});
```

## 资源管理

#### 1. 加载css

安装 style-loader css-loade
    
    yarn add style-loader css-loader -D

webpack.config.js

```
module.exports = {
   // ...
   module: {
     rules: [
       // ...
       {
         test: /\.css$/,
         use: [
           'style-loader',
           'css-loader'
         ]
       }
     ]
   }
};
```

#### 2. 加载图片、字体

安装 file-loader

    yarn add file-loader -D

webpack.config.js

```
module.exports = {
   // ...
   module: {
     rules: [
       // ...
       // 加载图片
       {
            test: /\.(png|svg|jpg|gif)$/,
            use: [
                'file-loader'
            ]
        },
        // 加载字体文件
        {
            test: /\.(woff|woff2|eot|ttf|otf)$/,
            use: [
            'file-loader'
            ]
        }
     ]
   }
};
```

#### 3. 加载数据

  csv-loader、xml-loader 可以处理CSV、TSV 和 XML这三类文件。

  安装 csv-loader、xml-loader

     yarn add csv-loader xml-loader -D

  webpack.config.js
```
module.exports = {
   // ...
   module: {
     rules: [
       // ...
       {
            test: /\.(csv|tsv)$/,
            use: [
                'csv-loader'
            ]
        },
        {
            test: /\.xml$/,
            use: [
                'xml-loader'
            ]
        }
     ]
   }
};
```


  [1]: https://lucinexl.github.io/2018/08/21/webpack-react/
  [2]: https://www.webpackjs.com/concepts/
