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

使用 Mocha 能够非常方便的测试异步代码。在你的测试完成后仅仅调用回调函数，通过向 ```it()``` 函数中添加一个回调函数（通常命名为 done）， mocha 就知道，应当等待这个函数被调用以完成这个测试。

```
describe('User', function() {
  describe('#save()', function() {
    it('should save without error', function(done) {
      var user = new User('Luna');
      user.save(function(err) {
        if (err) done(err);
        else done();
      });
    });
  });
});
```
为了让事情更加简单，我们使用 ```done()``` 回调函数时可以接受一个错误异常，所我我们可以直接使用：
```
describe('User', function() {
  describe('#save()', function() {
    it('should save without error', function(done) {
      var user = new User('Luna');
      user.save(done);
    });
  });
});
```

## 使用 Promises

 你可以选择返回 Promise 对象，来替代 ```done()``` 回调函数。在你测试 API 返回 promise 对象而不是接受一个回掉函数时十分有用：
 ```
 beforeEach(function() {
  return db.clear()
    .then(function() {
      return db.save([tobi, loki, jane]);
    });
});

describe('#find()', function() {
  it('respond with matching records', function() {
    return db.find({ type: 'User' }).should.eventually.have.length(3);
  });
});
 ```
 > 之后的示例将使用[Chai as Promised](karma_plugins_chai_promise.md)进行流畅的 promise 断言。
 在 Mocha 3.0.0 以上版本，返回一个 *Promise* 同时调用 *done()* 将会导致一个异常：
 
 ```
 const assert = require('assert');

it('should complete this test', function (done) {
  return new Promise(function (resolve) {
    assert.ok(true);
    resolve();
  })
    .then(done);
});
 ```
 上面的测试会抛出一个异常，```Error: Resolution method is overspecified. Specify a callback *or* return a Promise; not both.```。
 
# 同步代码测试

当测试同步代码，触发回调函数，Mocha 将会自动进行下一个测试。
```
describe('Array', function() {
  describe('#indexOf()', function() {
    it('should return -1 when the value is not present', function() {
      [1,2,3].indexOf(5).should.equal(-1);
      [1,2,3].indexOf(0).should.equal(-1);
    });
  });
});
```

# 钩子

Mocha 默认为 BDD 风格测试口，它提供了一组钩子 ```before(), after(), beforeEach(), afterEach()``` 。这些钩子可以用于创建预制条件并且在测试完成后清理它们。
```
describe('hooks', function() {

  before(function() {
    // 在当前代码块中所有测试运行前执行
    // runs before all tests in this block
  });

  after(function() {
    // 在当前代码块中所有测试运行后执行
    // runs after all tests in this block
  });

  beforeEach(function() {
    // 在当前代码块中每个测试运行前执行
    // runs before each test in this block
  });

  afterEach(function() {
    // 在当前代码块中每个测试运行后执行
    // runs after each test in this block
  });

  // test cases
});
```