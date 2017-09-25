# Files

files 选项决定了那些文件由浏览器引入那些文件由 karma 服务监控。

# 匹配模式与根路径

* 所有相对路径都会优先参考**basepath**进行解析。
* 如果**basepath**为相对路径，karma 会根据** configuration**所在路径进行解析。
* 最后所有的文件将根据[glob](https://github.com/isaacs/node-glob)进行匹配，所以你可使用例如test/unit/**/*.spec.js这样的表达式进行匹配。

# 排序

* 匹配模板的顺序决定了这些文件在浏览器中引入的顺序。
* 一个匹配模式匹配到多个文件时，按照字母排序进行排序。
* 每个文件只引入一次。如果多个模式匹配到同一文件，这个文件通过第一个匹配到它的模式引入。

# included，served，watched

每个模式不是一个简单的字符串就是一个包含4个属性的对象。

**pattern**
* 类型：string
* 无默认值
* 描述：用于匹配制定文件

**watched**
* 类型：Boolean
* 默认值： true
* 如果 **autowatch** 为 **true** 所有 **watched** 设置为 **true** 的匹配到的文件都会被 karma 监听 。

**included**
* 类型：Boolean
* 默认值：true
* 描述：匹配文件是否通过 **script** 标签引入浏览器，如果为 **false** 表示需要手动引入例如[Require.js](require.js.md)。

**served**
* 类型：Boolean
* 默认值：true
* 描述：文件是否由 Karma web 服务器提供

**nocache**
* 类型：Boolean
* 默认值：false
* 描述：是否每次都通过 karma web 服务获取文件。