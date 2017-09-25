# 预处理器

预处理器允许你对在文件被提供给浏览器前对它们做一些事情，这些配置在配置文件 ```preprocessors``` 字段中。
```
preprocessors: {
  '**/*.coffee': ['coffee'],
  '**/*.tea': ['coffee'],
  '**/*.html': ['html2js']
},
```