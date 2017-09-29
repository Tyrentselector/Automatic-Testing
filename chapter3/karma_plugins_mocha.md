# 简介

Mocha 是一款流行的js测试框架，它能够方便的创建测试套件、测试用例、测试规范。Mocha 可以在前端或者后端测试Typescript，指出性能问题，生成不同类型的测试报告。

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

## 对钩子函数的描述

每个钩子都可以传入一个可选的描述信息，它可以帮助你更准确的定位测试中的错误，如果钩子的回调函数是一个命名函数那么会使用它的函数名，否则会使用所提供的描述参数：
```
beforeEach(function() {
  // beforeEach hook
});

beforeEach(function namedFun() {
  // beforeEach:namedFun
});

beforeEach('some description', function() {
  // beforeEach:some description
});
```

## 异步钩子函数

所有的钩子函数可能是同步的也可能是异步的，例如你想在测试前使用虚假数据填充数据库：
```
let database = {};
function saveData(data, done) {
    setTimeout(function() {
        for (key in data) {
            database[key] = data[key];
        }
        console.log('log-----:data has saved!!');
        done();
    }, 1000);
}

function readData(key, cb) {
    setTimeout(function() {
        cb(database[key]);
    }, 1000);
}

let joh = {name: 'joh', age: 11};
let tim = {name: 'tim', age: 12};
let yeo = {name: 'yeo', age: 22};
beforeEach((done) => {
    console.log('log-----:begin save data!!');
    saveData([joh, tim, yeo], done);
});


describe('save data', () => {
    describe('read data', () => {
        it('respond with matching records', (done) => {
            readData(2, function(data) {
                console.log(`log-----: find data!!`, data);
                done();
            });
        });
        it('get matched data', () => {
            console.log(`log-----: data has get road!!`);
        });
    });
})
```

## root-level 钩子函数

你可以选择在任意文件中添加跟 **root-level** 钩子函数。例如，在所有 describe 代码块外部添加 ```forEach()```。这时无论在那个文件中的测试，将都会调用 ```forEach()```。
```
// test1.js
describe('save data', () => {
    it('begin save data', () => {
        console.log('log-----:data has saved!!');
    });
});

// test2.js
let test = require('./test1');

beforeEach(() => {
    console.log('log-----:begin save data!!');
});

describe('read data', () => {
    it('respond with matching records', () => {
        console.log(`log-----: find data!!`);
    });
    it('get matched data', () => {
        console.log(`log-----: data has get road!!`);
    });
})
```

## 延迟跟套件

如果你需要在你的测试套件运行前执行一些一部操作，你可以延迟跟套件执行。执行 mocha 时附加 --delay 参数。将会得到一个全局回调函数 run():
```
setTimeout(function() {
  // do some setup

  describe('my suite', function() {
    // ...
  });

  run();
}, 5000);
```
> 增加 --delay 参数后必须调用 run()。

# 待测试

待测试——没有提供回调函数的测试用例（最终会补全这个测试）：
```
describe('Array', function() {
  describe('#indexOf()', function() {
    // pending test below
    it('should return -1 when the value is not present');
  });
});
```
待测试同样会生成测试报告。

# 排他测试

通过添加 *.only()* 来调用函数排他属性允许你只运行指定的测试套件或测试用例。一个只执行指定测试套件的例子：
```
describe('Array', function() {
    describe.only('should execute suite', function() {
      // ...
      it('should execute case');
    });
    describe('should not execute suite', function() {
        // ...
        it('should not execute case');
      });
  });
  ```
  > 所有内部嵌套的套件依然会执行。

  一个只执行指定测试用例的例子：
  ```
  describe('Array', function() {
  describe('#indexOf()', function() {
    it.only('should return -1 unless present', function() {
      // ...
    });

    it('should return the index when present', function() {
      // ...
    });
  });
});
```

在3.0.0及后续版本中，*.only()* 可多次使用来指定多个需要测试的子集:
```
describe('Array', function() {
  describe('#indexOf()', function() {
    it.only('should return -1 unless present', function() {
      // this test will be run
    });

    it.only('should return the index when present', function() {
      // this test will also be run
    });

    it('should return -1 if called with a non-Array context', function() {
      // this test will not be run
    });
  });
});
```

你也可以选择多个测试套件：
```
describe('Array', function() {
  describe.only('#indexOf()', function() {
    it('should return -1 unless present', function() {
      // this test will be run
    });

    it('should return the index when present', function() {
      // this test will also be run
    });
  });

  describe.only('#concat()', function () {
    it('should return a new Array', function () {
      // this test will also be run
    });
  });

  describe('#slice()', function () {
    it('should return a new Array', function () {
      // this test will not be run
    });
  });
});
```

```
describe('Array', function() {
  describe.only('#indexOf()', function() {
    it.only('should return -1 unless present', function() {
      // this test will be run
    });

    it('should return the index when present', function() {
      // this test will not be run
    });
  });
});
```
> 如果有钩子函数，它依然会被执行。

# 除己测试

与排他测试 *.only()* 相反。通过添加 *.skip()*，忽略那些套件或用例。任何标记为 *skip* 的测试都会归类为[待测试](待测试用例)
