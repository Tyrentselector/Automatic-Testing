# 预处理器

预处理器允许你对在文件被提供给浏览器前对它们做一些事情，这些配置在配置文件 ```preprocessors``` 字段中。
```
preprocessors: {
  '**/*.coffee': ['coffee'],
  '**/*.tea': ['coffee'],
  '**/*.html': ['html2js']
},
```

# 可用预处理器

* [coffee](https://github.com/karma-runner/karma-coffee-preprocessor)
* [html2js](https://github.com/karma-runner/karma-html2js-preprocessor)
* [coverage](https://github.com/karma-runner/karma-coverage)
* [ng-html2js](https://github.com/karma-runner/karma-ng-html2js-preprocessor)
* [更多](https://www.npmjs.com/browse/keyword/karma-preprocessor)

# Mini matching

```preprocessors``` 配置对象的键用于过滤 ```files``` 中匹配到的文件。
例如路径 ```/my/absolute/path/to/test/unit/file.coffee``` 根据 ```**/*.coffee``` 进行匹配会返回 ```true```，但根据 ```*.coffee``` 匹配返回 ```false``` 预处理不会处理这些 coffee 文件。