# karma-webpack 简介

在 karma 中使用 webpack 与处理文件。

# 安装

```
npm i -D karma-webpack
```

# 配置

该配置可以创建一个 bundle，它包含了所有测试用例。使用改配置后不能运行单独测试用例。通过统一入口文件会引入所有测试套件并执行测试。

**karma.conf.js**

```
module.exports = (config) => {
  config.set({
    // ... normal karma configuration
    files: [
        // only specify one entry point
        // and require all tests in there
        'test/index_test.js'
    ],
 
    preprocessors: {
      // add webpack as preprocessor
      'test/index_test.js': [ 'webpack' ]
    },
 
    webpack: {
      // karma watches the test entry points
      // (you don't need to specify the entry option)
      // webpack watches dependencies
 
      // webpack configuration
    },
 
    webpackMiddleware: {
      // webpack-dev-middleware configuration
      // i. e.
      stats: 'errors-only'
    }
  })
}
```

**index_test.js**

```
// require all modules ending in "_test" from the
// current directory and all subdirectories
const testsContext = require.context(".", true, /_test$/)
 
testsContext.keys().forEach(testsContext)
```

# source map

我们可以使用 karma-source-loader 为我们生成的 bundle 加载 source map。

```
npm i -D karma-sourcemap-loader
```

**karma.conf.js**

```
preprocessors: {
  'test/test_index.js': [ 'webpack', 'sourcemap' ]
}
```

**webpack.config.js**

```
webpack: {
  // ...
  devtool: 'inline-source-map'
}
```
