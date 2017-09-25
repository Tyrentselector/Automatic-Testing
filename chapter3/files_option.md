# Files

files 选项决定了那些文件由浏览器引入那些文件由 karma 服务监控。

# 匹配模式与根路径

* 所有相对路径都会优先参考**basepath**进行解析。
* 如果**basepath**为相对路径，karma 会根据** configuration**所在路径进行解析。
* 最后所有的文件将根据[glob]()进行匹配，所以你可使用例如test/unit/**/*.spec.js这样的表达式进行匹配。
