# 文件匹配模式

所有制定文件路径的配置选项，使用[minimatch](https://github.com/isaacs/minimatch)库进匹配你想引入或排除的文件。

通过以下部分你能找到每个配置的细节，以下所有配置使用 minimatch 表达式：

* **exclude**
* **files**
* **preprocessors**

例如：

* ** \*\*/\*.js **: 所有子目录中所有以js为扩展名的文件
* _\* \_\*/!\(jquery\).js: 同上个例子相同，但是不包含“jquery.js”
* **\*\*/\(foo\|bar\).js**: 所有子目录中，所有“foo.js”和“bar.js”文件

