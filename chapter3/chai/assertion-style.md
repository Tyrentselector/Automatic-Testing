# 断言风格

在本章将为你介绍三种不同的在你的测试环境中使用的断言风格。当你决定使用那种风格后，我们将一起了解响应的 API 文档。

## Assert

[查看 Assert 风格 API 文档](http://chaijs.com/api/assert/)

```
var assert = require('chai').assert
  , foo = 'bar'
  , beverages = { tea: [ 'chai', 'matcha', 'oolong' ] };

assert.typeOf(foo, 'string'); // without optional message
assert.typeOf(foo, 'string', 'foo is a string'); // with optional message
assert.equal(foo, 'bar', 'foo equal `bar`');
assert.lengthOf(foo, 3, 'foo`s value has a length of 3');
assert.lengthOf(beverages.tea, 3, 'beverages has 3 types of tea');
```

## BDD

[查看 DBB 风格 API 文档](assertion-api.md)

BDD 风格有两种类型：```expect``` 和 ```should```。两种都是使用链式编程对断言进行构建，但是它们对断言的初始化构建方式不同。

### Expect

这种 BDD 风格的断言通过 ```expect``` 和 ```should``` 接口进行断言。在这两个场景中，你可以使用链式编程进行断言。

```
var expect = require('chai').expect
  , foo = 'bar'
  , beverages = { tea: [ 'chai', 'matcha', 'oolong' ] };

expect(foo).to.be.a('string');
expect(foo).to.equal('bar');
expect(foo).to.have.lengthOf(3);
expect(beverages).to.have.property('tea').with.lengthOf(3);
```
同时允许包含任意消息对任何可能发生的失败断言进行提示。
```
var answer = 43;

// AssertionError: expected 43 to equal 42.
expect(answer).to.equal(42);

// AssertionError: topic [answer]: expected 43 to equal 42.
expect(answer, 'topic [answer]').to.equal(42);
```

### Should

```should``` 风格断言同 ```expect``` 类型的一样使用链式断言。它为每一个对象扩展了一个 ```should``` 属性，并且将它作为链的断言链开始。这种风格在IE中会有一些问题，所以在使用时要注意浏览器的兼容性。
```
var should = require('chai').should() //actually call the function
  , foo = 'bar'
  , beverages = { tea: [ 'chai', 'matcha', 'oolong' ] };

foo.should.be.a('string');
foo.should.equal('bar');
foo.should.have.lengthOf(3);
beverages.should.have.property('tea').with.lengthOf(3);
```

### 两种风格的区别

首先，```expect``` 仅作为一个函数进行使用，而 ```should``` 的引入是一个被执行函数：
```
var chai = require('chai')
  , expect = chai.expect
  , should = chai.should();
```

### Should 额外注意事项

由于给定对象需要通过对 ```Object.property``` 进行扩展，所以在某些情况下 ```should``` 是不生效的。大体上，如果你尝试着去检查一个对象，使用下面的伪代码：
```
db.get(1234, function (err, doc) {
  // we expect error to not exist
  // we expect doc to exist and be an object
});
```
已知 ```err``` 是 undefined 或 null，```err.should.not.exist``` 是一个错误的声明，因为 ```undefined``` 或 ```null``` 没有 ```should``` 扩展属性。针对以上情况可以使用：
```
var should = require('chai').should();
db.get(1234, function (err, doc) {
  should.not.exist(err);
  should.exist(doc);
  doc.should.be.an('object');
});
```
可以使用一些快捷助手帮助你解决使用 ```should``` 时的障碍：
+ should.exist
+ should.not.exist
+ should.equal
+ should.not.equal
+ should.Throw
+ should.not.Throw
