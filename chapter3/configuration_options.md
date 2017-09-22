### 配置选项

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

描述：加载和捕获浏览器列表。当Karma启动后，它会启动在配置中配置所有浏览器。在Karma关闭的同时这些浏览器也会随之关闭。你可以打开浏览器并访问Karma web 服务器 [http://localhost:9876/](http://localhost:9876/) 手动捕获任何浏览器。

见[config/browsers](https://karma-runner.github.io/1.0/config/browsers.html)来获取更多信息。通过 [plugins](https://karma-runner.github.io/1.0/config/plugins.html) 可以定义其他加载器。使用**--no-browsers**命令行选项可以用空列表覆盖配置文件中的值。

### captureTimeout

类型：Number  
默认值：60000  
描述：捕获浏览器超时时长。captureTimeout 值代表Karma允许浏览器启动并链接到Karma服务器的最大时常。如果任何浏览器在规定时间内没有被捕获到。将会再一次进行链接，在尝试三次后Karma会放弃尝试。

### client.args

类型：Array  
默认值：undefined  
CLI：所有参数前加--（只有再运行 karma run 时生效）  
描述：在命令行中执行**karma run**并传入额外参数，它们作为**karma.config.args**通过测试适配器被传入。**client.args**选项允许你设定除了**run**之外的动作值。至于这些值如何被用于你的测试适配器，你可以通过设配器获取相关信息。

### client.useIframe

类型：Boolean  
默认值：true  
描述：在新窗口或iFrame中运行测试，为true时Karma在iFrame中运行测试，如果为false则在新窗口中运行。

### client.runInParent

类型：Boolean  
默认值：false  
描述：在当前客户端同一窗口中运行测试，不使用iFrame或开启新窗口。

### client.captureConsole

类型：Boolean  
默认值：true  
描述：捕获所有控制台输出并发送到终端中。

### client.clearContext

类型： Boolean  
默认值：true  
描述：如果为 true Karma 在完成测试后清空window环境上下文。

### colors

类型：Boolean  
默认值：true  
CLI：--colors，--no-colors  
描述：开启或禁用输出报告或日志中的颜色

### concurrency

类型：Number
默认值：Infinity
描述：Karma同时加载浏览器个数

### crossOriginAttribute

类型：Boolean
默认值：true
描述：当为 true 时将会添加 crossorigin 属性到生成的 script 标签中。为跨域 js 文件提供更好的错误报告。当你加载额外的 script 脚本并且这些脚本不需要**Access-Control-Allow-Origin**请求头的时可以禁用这个选项。

### customContextFile

类型：string
默认值：null
描述：如果为null，karma会使用自己的context.html文件。

### customDebugFile

类型：string
默认值：null
描述：如果为null，karma会使用自己的debug.html文件。

### customClientContextFile

类型：string
默认值：null
描述：如果为null，karma会使用自己的client_with_context.html文件（这个文件会在 client.runInParent 设置为 true 时使用）。

### customHeaders

类型：Array
默认值：undefined
描述：自定义 HTTP 头会通过 Karma 的 web 服务器设置在服务文件中。它是十分有用的一个配置，尤其是对于即将到来的一些浏览器功能例如Service Workers。
**customHeaders** 允许为正则表达式匹配到的文件设定 HTTP 头。**customHeaders** 是一个包含以下属性的对象数组：
* match：用于匹配文件的正则表达式
* name：HTTP 响应头字段名
* **例如：**
```
customHeaders: [{
  match: '.*foo.html',
  name: 'Service-Worker-Allowed',
  value: '/'
}]
```

### detached

类型：Boolean
默认值：false
CLI：--detached
描述：当为 true 时将会在一个新线程中开启 karma 服务器，控制台不写入输出。这个服务器可以通过 **karma stop** 命令停止服务。

### exclude

类型：Array
默认值：[]
描述：要排除文件的一个文件列表或匹配模式。

### failOnEmptyTestSuite

类型：Boolean
默认值：true
CLI：--fail-on-empty-test-suite, --no-fail-on-empty-test-suite
描述：开启或禁用，当运行空测试套件时失败。如果禁用程序会返回一个退出代码**0**并且展示一个警告。

### files

类型：Array
默认值：[]
描述：需要在浏览器中加载的文件的文件列表或匹配方式

### forceJSONP

类型：Boolean
默认值：false
描述：强制 socket.io 使用 JSONP 轮询替代 XHR 轮询。

### frameworks

类型：Array
默认值：[]
描述：你想要使用的测试框架列表。你可能会设置为['jasmine'], ['mocha'] 或 ['qunit'] 等等。
>以上所有的测试框架或插件都需要通过Npm进行安装后才能使用。

### listenAddress

类型：string
默认值：'0.0.0.0' 或 LISTEN_ADDR
描述：服务器监听地址。变更为“localhost”仅监听回路，或“::”监听所有IPv6接口。

### hostname

类型：string
默认值：localhost
描述：hostname 在捕获浏览器时使用。

### httpsServerOptions

类型：对象
默认值：{}
描述：选项对象会被 Node 的 https 类使用。

### logLevel

类型：Constant
默认值：config.LOG_INFO
CLI: --log-level debug
**可选值：**
* config.LOG_DISABLE
* config.LOG_ERROR
* config.LOG_WARN
* config.LOG_INFO
* config.LOG_DEBUG

描述：日志等级

### loggers

类型：Array
默认值：[{type: 'console'}]
描述：日志输出源要使用的列表，更多信息详见[log4js](https://github.com/nomiddlename/log4js-node)

### middleware

类型：Array
默认值:[]
描述：karma 服务器需要使用的附加中间件名称列表。中间件会按照列出顺序使用。
你必须通过 npm 安装你所需的中间件。通过 [plugins](karma_plugins.md)更多信息。

这种插件必须提供一个 express/connect 中间件函数（更多细节请参考 [Express 文档](https://expressjs.com/en/guide/using-middleware.html)）。自定义内联中间件如下所示：
```
var CustomMiddlewareFactory = function (config) {
  return function (request, response, /* next */) {
    response.writeHead(200)
    return response.end("content!")
  }
}
middleware: ['custom']
plugins: [
  {'middleware:custom': ['factory', CustomMiddlewareFactory]}
  ...
]
```

### mime

类型：Object
默认值：{}
描述：从新定义文件扩展名到 MIME-Type 的默认映射。属性设定为所需的 MIME，提供一个扩展名列表作为值。
**Example：**
```
mime: {
   'text/x-typescript': ['ts','tsx']
   'text/plain' : ['mytxt']
}
```
### plugins

类型：Array
默认值：['karma-*']
描述：加载插件列表。一个插件可以是一个字符串或一个内联插件对象。默认情况下，Karma 会加载 modules 目录下所有以 **karma-\*** 开头的组件。
参考[plugins](karma_plugins.md)获取更多信息。

### port

类型：Number
默认值：9876
CLI：--port 9876
描述：web 服务监听端口。

### processKillTimeout

类型：Number
默认子：2000
描述：在发送 SIGKILL 信号前 karma 等待浏览器进程终止时长，
如果在测试执行完成后，或 Karma 视图关闭浏览器，浏览器在 processKillTimeout 规定时间内没有关闭，Karma 将会发送 SIGKILL 信号尝试强制关闭浏览器。

### preprocessors

类型：Object
默认值：{'**/*.coffee': 'coffee'}
描述：一个将要使用预处理器的映射。
预处理器可能会改变运行时可用文件的文件类型及内容，例如如果你对你的源文件使用了 “coverage” 预处理器，当你试着交互式的调试你的测试时，你会发现你的源代码已经完全改变了，因为你想要处理这些文件以至于你在“reporters”列表中自动构建并使用了 “coverage” 预处理器入口，但是你的交互式调试没有。

### reportSlowerThan

类型：Number
默认值：0
描述：karma 将会报告所有比给定时间慢的测试。默认情况是禁用的。

### reporters

类型：Array
默认值：['progress']
描述：要使用的报告列表
其他的报告器，例如 **growl, junit, teamcity 或 coverage** 能够通过[插件](karma_plugins.md)加载。

### restartOnFileChange

类型：Boolean
默认值： false
描述：karma 监听文件改变，它会在当前测试执行完毕后开始一个新的测试。restartOnFileChange 为 true 时，当 karma 监听到文件改变后立即取消当前执行测试然后开始一个新的测试。

### retryLimit

类型：Number
默认值：2
描述：当浏览器宕机后，karma 会尝试重现新加载浏览器。这个参数标识 karma 尝试重新加载的次数。

### singleRun

类型：Boolean
默认值：false
CLI：--single-run, --no-single-run
描述：持续集成模式。
如果为 true，karma将会开启并捕获所有配置的浏览器，运行测试，然后根据测试结果返回 0 或 1，0 表示所有测试全部通过，1 表示有测试失败了。