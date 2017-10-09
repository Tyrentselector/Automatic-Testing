# API Reference

## 语法链

以下提供的一些链式获取器来提升断言的可读性：

Chains
+ to
+ be
+ been
+ is
+ that
+ which
+ and
+ has
+ have
+ with
+ at
+ of
+ same
+ but
+ does

### .not

否定当前断言链中之后的所有断言。
```
expect(function () {}).to.not.throw();
expect({a: 1}).to.not.have.property('b');
expect([1, 2]).to.be.an('array').that.does.not.include(3);
```
你可以通过 ```.not``` 否定任何断言，但并不意味着你应该使用他。功能越强大伴随的责任也就越大。最好为你的断言提供一个你期望得到的值，而不是在一堆无用值中排除你不想要的。
```
expect(2).to.equal(2); // Recommended
expect(2).to.not.equal(1); // Not recommended
```

### .deep

所有 ```.equal```, ```.include```, ```.members```, ```.keys``` 和 ```.property``` 在 deep 之后的断言表示深度等于而不是严格等于。
```
// Target object deeply (but not strictly) equals `{a: 1}`
expect({a: 1}).to.deep.equal({a: 1});
expect({a: 1}).to.not.equal({a: 1});

// Target array deeply (but not strictly) includes `{a: 1}`
expect([{a: 1}]).to.deep.include({a: 1});
expect([{a: 1}]).to.not.include({a: 1});

// Target object deeply (but not strictly) includes `x: {a: 1}`
expect({x: {a: 1}}).to.deep.include({x: {a: 1}});
expect({x: {a: 1}}).to.not.include({x: {a: 1}});

// Target array deeply (but not strictly) has member `{a: 1}`
expect([{a: 1}]).to.have.deep.members([{a: 1}]);
expect([{a: 1}]).to.not.have.members([{a: 1}]);

// Target set deeply (but not strictly) has key `{a: 1}`
expect(new Set([{a: 1}])).to.have.deep.keys([{a: 1}]);
expect(new Set([{a: 1}])).to.not.have.keys([{a: 1}]);

// Target object deeply (but not strictly) has property `x: {a: 1}`
expect({x: {a: 1}}).to.have.deep.property('x', {a: 1});
expect({x: {a: 1}}).to.not.have.property('x', {a: 1});
```
