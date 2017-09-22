# 配置选项

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

类型：对象
默认值：{level: "debug", format: "%b %T: %m", terminal: true}
描述：配置浏览器控制台如何输出日志，以下属性均为可选项：
```
{
  // level 期望输出那个等级的日志
  level:  string,
  // format 版式字符串，%b, %t, %T, %m，分别被浏览器字符串，小写日志类型，大写日志类型和日志消息替换，格式化器只会影响到输出文件。
  format: string, 
  //path 为输出文件的输出路径。
  path:   string,
  terminal: boolean
}
```




