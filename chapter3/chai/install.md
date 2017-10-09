# 简介

Chai 是一款 BDD/TDD 断言库可用于 node 和浏览器环境，并且可以和任何 javascript 测试框架轻松适配。

# 安装

## Node.js

通过 npm 安装：
```
npm install chai
```

推荐以```*```作为值添加至 ```package.json``` 的 *devDependencies* 项中。通过执行 ```npm install``` 命令安装最新版本。当与持续集成工具配合使用时更为强大：
```
"devDependencies": {
  "chai": "*",
  "mocha": "*"
}, "//": "mocha is our preference, but you can use any test runner you like"
```

## Browser

通过 ```script``` 标签引入：
```<script src="chai.js" type="text/javascript"></script>```
```chai``` 将作为全局对象存在，或通过 AMD 规范引入。




