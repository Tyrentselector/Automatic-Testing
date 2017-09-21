# Karma

[karma](https://karma-runner.github.io/1.0/index.html)是一个测试运行器，我们将使用它自动执行测试。它能够被持续集成构建服务触发。
karma可以通过插件与多种测试框架配合使用。karma运行在node.js环境上，可以通过NPM获取。

## 安装

### 安装node.js

我们推荐Mac和linux通过[NVM](https://github.com/creationix/nvm)安装node.js。在window系统中从[官方网站](https://nodejs.org/en/)中获取node.js安装环境。

> 注意：karma可以在 Node.js 0.10, 0.12.x, 4.x, 5.x, 6.x, 和 7.x中运行。

-----

### 安装karma及插件

-----
我们推荐将karma安装到项目目录本地。

```
# 安装 Karma:
$ npm install karma --save-dev

# 安装项目所需插件:
$ npm install karma-mocha karma-coverage --save-dev
```
npm会把karma karma-mocha karam-coverage 包安装到当前工作目录中**node_modules**目录中，同时将作为依赖项保存到**package.json**中的**devDependencies**字段中。以便其他开发人员直接可以直接通过**npm install**命令直接安装所有依赖。

```
# 运行 Karma:
$ ./node_modules/karma/bin/karma start
```
-----
### 命令行接口

每次输入*./node_modules/karma/bin/karma start*是不是很不爽？如果你想在windows系统中随时通过命令行启动karma只需要执行：

```
$ npm install -g karma-cli
```

这样你就可以通过简单的**karma**命令在任何地方运行karma了，同时它总是运行本地版本。

-----
