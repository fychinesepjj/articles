# webpack升级2.0注意事项

## 语法
1. 支持原生ES6模块加载语法`import`, `export`, `System.import`
2. 支持ES6和AMD,CommandJs一起使用
3. webpack配置`resolve`节点发生变化：

    ```javascript
    // webpack 1.0
    resolve: {
        root: [config.mediaDir, config.nodeModPath],
        alias: config.pathMap,
        extensions: ['', '.js']
    }
    ...
    // webpack 2.0
    resolve: {
        modules: [config.mediaDir, config.nodeModPath],
        descriptionFiles: ['package.json'],
        alias: config.pathMap,
        extensions: ['', '.js'],
        moduleExtensions: ["-loader"]
    }
    ```

## 插件
* `webpack.optimize.OccurenceOrderPlugin` => `webpack.optimize.OccurrenceOrderPlugin` 修复命名错误。
* `ExtractTextPlugin`需要更新到支持`webpack2`版本，并且语法发生变化。

    ```javascript
    // webpack 1.0
    ExtractTextPlugin.extract('style', 'css?minimize!sass', {publicPath: "../"});

    // webpack 2.0
    ExtractTextPlugin.extract({fallbackloader: 'style-loader', loader: 'css?minimize!sass', publicPath: "../"});
    ```

## 参考
* [webpack2.0 变化（英）](https://gold.xitu.io/entry/56b0623cc14061005a028d08)
* [webpack2.0 变化（中）](https://mp.weixin.qq.com/s?__biz=MzIyMjE0ODQ0OQ==&mid=402764877&idx=1&sn=aa40a80bb1920a80fc187e8df99c4824)
* [webpack2.0 优化](http://www.open-open.com/lib/view/open1483317889255.html)