# Karma

[karma](https://karma-runner.github.io/1.0/index.html)是一个测试运行器，我们将使用它自动执行测试。它能够被持续集成构建服务触发。
karma可以通过插件与多种测试框架配合使用。karma运行在node.js环境上，可以通过NPM获取。

## 安装

### 安装node.js

-----
我们推荐Mac和linux通过[NVM](https://github.com/creationix/nvm)安装node.js。在window系统中从[官方网站](https://nodejs.org/en/)中获取node.js安装环境。

> 注意：karma可以在 Node.js 0.10, 0.12.x, 4.x, 5.x, 6.x, 和 7.x中运行。

### 安装karma及插件

我们推荐将karma安装到项目目录本地。

```
# 安装 Karma:
$ npm install karma --save-dev

# 安装项目所需插件:
$ npm install karma-jasmine karma-chrome-launcher jasmine-core --save-dev

```