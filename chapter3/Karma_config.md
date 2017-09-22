# 配置

通过配置文件可以让karma了解你的项目从而提供更好的服务，本章阐述了如何创建一个配置文件。

> 大多数适配器、报告器、预处理器和加载器框架都需要以插件的形式引入。

## 创建配置文件

通过**karma init**我们可以快速创建一个配置文件：

```
$ karma init my.conf.js

Which testing framework do you want to use?
你想要使用那个测试框架？
Press tab to list possible options. Enter to move to the next question.
按下Tab键显示可选列表。Enter键进行下一步。
> mocha

Do you want to use Require.js?
是否使用 Require.js？
This will add Require.js plugin.
这将会添加 Require.js 插件
Press tab to list possible options. Enter to move to the next question.
按下Tab键显示可选列表。Enter键进行下一步。
> no

Do you want to capture a browser automatically?
是否希望自动指定一个浏览器？
Press tab to list possible options. Enter empty string to move to the next question.
按下Tab键显示可选列表。Enter键进行下一步。
> Chrome
> Firefox
>

What is the location of your source and test files?
你的源文件及测试文件路径所处位置？
You can use glob patterns, eg. "js/*.js" or "test/**/*Spec.js".
你能够是用 glob 模式，例如 "js/*.js" 或 "test/**/*Spec.js"。
Press Enter to move to the next question.
> *.js
> test/**/*.js
>

Should any of the files included by the previous patterns be excluded?
通过之前匹配模式匹配到的文件，是否有需要排除掉的？
You can use glob patterns, eg. "**/*.swp".
可以使用 glob 模式，例如 "**/*.swp" 进行排除。
Press Enter to move to the next question.
>

Do you want Karma to watch all the files and run the tests on change?
是否希望karma检测到文件变动后自动运行测试？
Press tab to list possible options.
> yes

Config file generated at "/Users/vojta/Code/karma/my.conf.js".
配置文件已经生成，路径"/Users/vojta/Code/karma/my.conf.js"。
```

我们可以手动编写配置文件或者从其他项目拷贝一份。

Karma 配置文件可以使用 JavaScript、CoffeeScript，TypeScript编写并且作为一个标准node模块加载。

如果不提供参数，Karma将会以一下顺序搜索配置文件：

* **./karma.conf.js**
* **./karma.conf.coffee**
* **./karma.conf.ts**
* **./.config/karma.conf.js**
* **./.config/karma.conf.coffee**
* **./.config/karma.conf.ts**

配置文件内部，配置代码全部在**module.exports**指向的一个接受一个配置对象的函数中。

```
// karma.conf.js
module.exports = function(config) {
  config.set({
    basePath: '../..',
    frameworks: ['jasmine'],
    //...
  });
};
```

## 配置选项

以下包涵所有可用配置选项。

### 自动监听

类型：Boolean

默认值：true

CLI：--auto-watch, --no-auto-watch

描述：启用或关闭，监听文件变更后自动执行测试功能。

### 自动监听延迟

类型：Number

默认值：250

描述：该配置项告诉Karma在监听到文件发生变更后再次运行测试等待时常。

### 根路径

类型：String

默认值：' '

描述：用于定义**files**和**exclude**相对路径的根路径，如果basePath为相对路径那么它将会被转换为配置文件所在路径**\_\_dirname**。

### 浏览器离线超时

类型：Number

默认：2000

描述：Karma等待浏览器重连时常。

### 浏览器控制台日志输出配置





