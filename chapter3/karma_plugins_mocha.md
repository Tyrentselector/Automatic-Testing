# 安装
全局安装
```
$ npm install --global mocha
```

或安装到你的项目中
```
$ npm install --save-dev mocha
```

# 快速上手

```
$ npm install mocha
$ mkdir test
$ $EDITOR test/test.js # or open with your favorite editor
```

在编辑器中：

```
var assert = require('assert');
describe('Array', function() {
  describe('#indexOf()', function() {
    it('should return -1 when the value is not present', function() {
      assert.equal(-1, [1,2,3].indexOf(4));
    });
  });
});
```

在命令行中执行
```
$ mocha

$ Array
$    #indexOf()
$      √ should return -1 when the value is not present

$  1 passing (13ms)
```

# 断言库

mocha 允许你使用你期望的断言库，上面的例子我们使用的是内置断言库，在我们的测试过程中使用的是 [**chai**](/karma_plugins_assert.md) 作为断言库。

# 异步代码

使用 Mocha 能够非常方便的测试异步代码。在你的测试完成后仅仅调用回调函数，通过向 ```it()``` 函数中添加一个回调函数（通常命名为 done）， mocha 就知道，应当等待这个函数被调用来完成这个测试。


