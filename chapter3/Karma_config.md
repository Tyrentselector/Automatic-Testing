# 配置

通过配置文件可以让karma了解你的项目从而提供更好的服务，本章阐述了如何创建一个配置文件。

## 创建配置文件

通过**karma init**我们可以快速创建一个配置文件：

```
$ karma init my.conf.js

Which testing framework do you want to use?
Press tab to list possible options. Enter to move to the next question.
> mocha

Do you want to use Require.js?
This will add Require.js plugin.
Press tab to list possible options. Enter to move to the next question.
> no

Do you want to capture a browser automatically?
Press tab to list possible options. Enter empty string to move to the next question.
> Chrome
> Firefox
>

What is the location of your source and test files?
You can use glob patterns, eg. "js/*.js" or "test/**/*Spec.js".
Press Enter to move to the next question.
> *.js
> test/**/*.js
>

Should any of the files included by the previous patterns be excluded?
You can use glob patterns, eg. "**/*.swp".
Press Enter to move to the next question.
>

Do you want Karma to watch all the files and run the tests on change?
Press tab to list possible options.
> yes

Config file generated at "/Users/vojta/Code/karma/my.conf.js".
```