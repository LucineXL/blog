---
title: 基于webpack4搭建一个简单的React脚手架 （三）
date: 2018-09-05 16:46:53
tags:
    - React
    - webpack
cover: https://images.pexels.com/photos/1203309/pexels-photo-1203309.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=750&w=1260
---


### 往期文章地址
  [<font color=#518dca>基于 webpack4 搭建 一个简单 的 React 脚手架 （一）</font>][1]
  [<font color=#518dca>基于 webpack4 搭建 一个简单 的 React 脚手架 （二）</font>][2]

  [<font color=#518dca>项目git地址</font>][0]

  [<font color=#518dca>webpack4 官方文档 ，请戳这里~</font>][3]


## 1. typeScript

  关于 typeScript 是个什么东西， 在这里就不赘述了， [<font color=#518dca>中文文档 ，戳这里~</font>][4]
 
  安装
    
    yarn add  typescript @types/react @types/react-dom awesome-typescript-loader source-map-loader -D

  添加 tsconfig.json 文件, 详细信息看[这里][5]
```
{
  "compilerOptions": {
    "outDir": "./dist/",
    "sourceMap": true,
    "noImplicitAny": true,
    "module": "commonjs",
    "target": "es5",
    "jsx": "react"
  },
  "include": [
      "./src/**/*"
  ]
}

```

  新建一个组件

  hello.tsx

```
import * as React from 'react';
export interface Props {
  name: string;
  enthusiasmLevel?: number;
}

export default class Hello extends React.Component<Props, {}> {
  render() {
    const { name, enthusiasmLevel = 1 } = this.props;

    if (enthusiasmLevel <= 0) {
      throw new Error('You could be a little more enthusiastic. :D');
    }

    return (
      <div className="hello">
        <div className="greeting">
          Hello {name + getExclamationMarks(enthusiasmLevel)}
        </div>
      </div>
    );
  }
}

function getExclamationMarks(numChars: number) {
  return Array(numChars + 1).join('!');
}
```


index.tsx

```
import * as React from 'react';
import * as ReactDom from 'react-dom';
import './index.scss';
import Hello from "./hello";
const logo = require('./logo.png');

export class Root extends React.Component<{}, {}> {
    render() {
        return (
          <div>
            我是 root
            <Hello name="TypeScript" enthusiasmLevel={10} />
            <img src={logo} />
          </div>
        )
    }
}

ReactDom.render(
  <Root />,
  document.getElementById('root')
)
```


webpack.common.js

```
module.exports = {
    entry: "./src/index.tsx",
    output: {
        filename: "bundle.js",
        path: __dirname + "/dist"
    },

    // Enable sourcemaps for debugging webpack's output.
    devtool: "source-map",

    resolve: {
        // Add '.ts' and '.tsx' as resolvable extensions.
        extensions: [".ts", ".tsx", ".js", ".json"]
    },

    module: {
        rules: [
            // All files with a '.ts' or '.tsx' extension will be handled by 'awesome-typescript-loader'.
            { test: /\.tsx?$/, loader: "awesome-typescript-loader" },

            // All output '.js' files will have any sourcemaps re-processed by 'source-map-loader'.
            { enforce: "pre", test: /\.js$/, loader: "source-map-loader" }
        ]
    },
};
```


  [0]: https://github.com/LucineXL/webpackAndReact
  [1]: https://lucinexl.github.io/2018/08/21/webpack-react/
  [2]: https://lucinexl.github.io/2018/08/27/webpack-react2/
  [3]: https://www.webpackjs.com/concepts/
  [4]: https://www.tslang.cn/
  [5]: https://www.tslang.cn/docs/handbook/tsconfig-json.html
