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
