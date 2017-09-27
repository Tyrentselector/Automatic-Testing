# 插件

Karma 可以轻松通过插件进行扩展。事实上所有现有的预处理器、报告器、浏览器记载器及测试框架都是插件。

# 插件的安装

插件是 Npm 模块，所以推荐通过在 ```package.json``` 中添加依赖，进行安装。
```
{
  "devDependencies": {
    "karma": "~0.10",
    "karma-mocha": "~0.0.1",
    "karma-growl-reporter": "~0.0.1",
    "karma-firefox-launcher": "~0.0.1"
  }
}
```
因此，可以通过以下方式进行安装：
```
npm install karma-<plugin name> --save-dev
```

# 加载插件

默认情况下 Karma 加载所有 npm 模块下所有以 ```karma-*``` 开头的兄弟模块。