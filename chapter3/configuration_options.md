# 配置选项

以下包涵所有可用配置选项。

### autoWatch

类型：Boolean

默认值：true

CLI：--auto-watch, --no-auto-watch

描述：启用或关闭，监听文件变更后自动执行测试功能。

### autoWatchBatchDelay

类型：Number

默认值：250

描述：该配置项告诉Karma在监听到文件发生变更后再次运行测试等待时常。

### basePath

类型：String

默认值：' '

描述：用于定义**files**和**exclude**相对路径的根路径，如果basePath为相对路径那么它将会被转换为配置文件所在路径**\_\_dirname**。

### browserDisconnectTimeout

类型：Number

默认：2000

描述：Karma等待浏览器重连时常。

### browserConsoleLogOptions

类型：对象  
默认值：{level: "debug", format: "%b %T: %m", terminal: true}  
描述：配置浏览器控制台如何输出日志，以下属性均为可选项：

```
{
  // level 期望输出那个等级的日志
  level:  string,
  // format 版式字符串，%b, %t, %T, %m，分别被浏览器字符串，小写日志类型，大写日志类型和日志消息替换，格式化器只会影响到输出文件
  format: string, 
  // path 为输出文件的输出路径
  path:   string,
  // terminal 表示日志是否写入终端
  terminal: boolean
}
```

### browserDisconnectTolerance

类型：Number  
默认值：0  
描述：浏览器与Karma服务器链接异常容忍失次数。

### browserNoActivityTimeout

类型：Number  
默认值：10000  
描述：在与浏览器断开链接前，karma等待浏览器响应最大时常。如果在测试执行期间，Karma在browserNoActivityTimeout指定时间内没有接收到任何来自浏览器的消息时将会与浏览器断开链接。

### browsers

类型：Array  
默认值：\[\]  
CLI：--browsers Chrome,Firefox, --no-browsers  
**可能值：**

* **Chrome** \(加载器需要 karma-chrome-launcher 插件\)
* **PhantomJS** \(加载器需要 requires karma-phantomjs-launcher 插件\)
* **Firefox** \(加载器需要 karma-firefox-launcher 插件\)
* **Opera** \(加载器需要 karma-opera-launcher 插件\)
* **IE** \(加载器需要 karma-ie-launcher 插件\)
* **Safari** \(加载器需要 requires karma-safari-launcher 插件\)
  
描述：加载和捕获浏览器列表。当Karma启动后，它会启动在配置中配置所有浏览器。在Karma关闭的同时这些浏览器也会随之关闭。你可以打开浏览器并访问Karma web 服务器 http://localhost:9876/ 手动捕获任何浏览器。

见[config/browsers](https://karma-runner.github.io/1.0/config/browsers.html)来获取更多信息。通过 [plugins](https://karma-runner.github.io/1.0/config/plugins.html) 可以定义其他加载器。使用**--no-browsers**命令行选项可以用空列表覆盖配置文件中的值。

### captureTimeout

类型：Number
默认值：60000
描述：捕获浏览器超时时长。captureTimeout 值代表Karma允许浏览器启动并链接到Karma服务器的最大时常。如果任何浏览器在规定时间内没有被捕获到。将会再一次进行链接，在尝试三次后Karma会放弃尝试。

### client.args
类型：Array
默认值：undefined
CLI：所有参数后--（只有再运行 karma run 时生效）
