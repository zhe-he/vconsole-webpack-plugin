# vconsole-webpack-plugin
webpack plugin for vConsole

## 安装

```bash
npm install vconsole-webpack-plugin --save-dev
```

## 使用

`webpack.conf.js` 文件配置里增加以下插件配置即可

```js
module.exports = {
    ...

    plugins: [
        new require("vconsole-webpack-plugin")({
        	enable: true // 发布代码前记得改回 false
        }),
        ...
    ]
    ...
}
```

注意，`vConsole` 作为一个调试模块，注定了需要在发布前把它去掉，为了避免人为操作失误而影响线上功能，这里建议配置如下：

`package.json` 文件配置：

```json
scripts: {
	"dev": "webpack -w --debug",
	"prod": "webpack -p"
}
```

`webpack.conf.js` 配置：

```js
// 接收运行参数
const argv = require('yargs')
	.describe('debug', 'debug 环境') // use 'webpack --debug'
	.argv;

module.exports = {
    ...

    plugins: [
        new require("vconsole-webpack-plugin")({enable: !!argv.debug}),
        ...
    ]
    ...
}
```

这样，在开发的时候运行 `npm run dev`，发布的时候运行 `npm run prod` 即可。

## 例子参考: [webpack-demo](https://github.com/diamont1001/webpack-demo/tree/master/example1)
