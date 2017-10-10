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

### .nested

在之后的所有 ```.include``` 和 ```.property``` 断言中可以使用点中括号记号法：
```
expect({a: {b: ['x', 'y']}}).to.have.nested.property('a.b[1]');
expect({a: {b: ['x', 'y']}}).to.nested.include({'a.b[1]': 'y'});
```
如果，```.``` 或 ```[]``` 属性名的一部分，可以通过在之前添加添加两个反斜杠进行转译：
```
expect({'.a': {'[b]': 'x'}}).to.have.nested.property('\\.a.\\[b\\]');
expect({'.a': {'[b]': 'x'}}).to.nested.include({'\\.a.\\[b\\]': 'x'});
```
```.nested``` 不能和 ```.own``` 联用。

###.own

会引起之后的所有 ```.property``` 和 ```.include``` 断言忽略继承属性：
```
Object.prototype.b = 2;

expect({a: 1}).to.have.own.property('a');
expect({a: 1}).to.have.property('b').but.not.own.property('b'); 

expect({a: 1}).to.own.include({a: 1});
expect({a: 1}).to.include({b: 2}).but.not.own.include({b: 2});
```
```.own``` 不能和 ```.nested``` 联用。

### .order

要求之后的所有 ```.member``` 断言中，所有期望值成员的顺序与实际值的成员顺序相同。
```
expect([1, 2]).to.have.ordered.members([1, 2])
  .but.not.have.ordered.members([2, 1]);
```
当 ```.include``` 和 ```.order``` 联合使用时，顺序对比始于这两个数组的头部。
```
expect([1, 2, 3]).to.include.ordered.members([1, 2])
  .but.not.include.ordered.members([2, 3]);
```

### .any

之后所有 ```.keys``` 断言仅要求目标含有一个所给键。与 ```.all``` 相反，all 要求目标拥有所有给定键。
```
expect({a: 1, b: 2}).to.not.have.any.keys('c', 'd');
```

### .all

之后所有 ```.keys``` 断言仅要求目标含有所有指定点给键。与 ```.any``` 相反，any 要求目标拥有至少一个给定键。
```
expect({a: 1, b: 2}).to.have.all.keys('a', 'b');
```
注意既没有使用 ```.all``` 或 ```.any``` 时，默认直接使用 ```.all```，为了良好的可读性最好使用 ```.all```。

### .a(type[,msg])

+ @param { String } type
+ @param { String } msg _optional_

用于断言目标类型是否为指定类型，忽略大小写。
```
expect('foo').to.be.a('string');
expect({a: 1}).to.be.an('object');
expect(null).to.be.a('null');
expect(undefined).to.be.an('undefined');
expect(new Error).to.be.an('error');
expect(Promise.resolve()).to.be.a('promise');
expect(new Float32Array).to.be.a('float32array');
expect(Symbol()).to.be.a('symbol');
```
```.a``` 支持对象通过 ```Symbol.toStringTag``` 定义自定义类型。
```
var myObj = {
  [Symbol.toStringTag]: 'myCustomType'
};

expect(myObj).to.be.a('myCustomType').but.not.an('object');
```
在对同一目标进行更多检测时最好对先使用 ```.a``` 对它进行类型检测。这样能够避免来自任何断言的无法预料的行为。这些断言会根据目标类型作不同的事。
```
expect([1, 2, 3]).to.be.an('array').that.includes(2);
expect([]).to.be.an('array').that.is.empty;
```
可以通过在链中添加 ```.not``` 来否定 ```.a```。然而最好断言目标期望类型，而不是断言目标类型不是众多不期望类型中的一个。
```
expect('foo').to.be.a('string'); // Recommended
expect('foo').to.not.be.an('array'); // Not recommended
```
```.a``` 可以接收一个可选参数 ```msg```，```msg``` 是一个自定义错误信息，当断言失败时显示。这个消息同样可以作为 ```expect``` 的第二参数。
```
expect(1).to.be.a('string', 'nooo why fail??');
expect(1, 'nooo why fail??').to.be.a('string');
```
同时 ```.a``` 可以提升断言的可读性。
```
expect({b: 2}).to.have.a.property('b');
```
别名```.an``` 可以替换 ```.a``` 使用。

### .include(val[, msg])

+ @param { Mixed } val
+ @param { String } msg _optional_

当目标是一个字符串时，```.include``` 断言所给值 ```val``` 是否为目标字符串的一个子串。
```
expect('foobar').to.include('foo');
```

当目标是一个数组时，```.include``` 断言所给值 ```val``` 是否为目标的一个成员。
```
expect([1, 2, 3]).to.include(2);
```

当目标是一个对象时，```.include``` 断言所给值 ```val``` 的属性是否为目标对象属性的子集。
```
expect({a: 1, b: 2, c: 3}).to.include({a: 1, b: 2});
```

当目标是 Set 或 WeakSet 时，```.include``` 断言所给值 ```val``` 是否为目标对象成员。
```
expect(new Set([1, 2])).to.include(2);
```

当目标是 Map 时，```.include``` 断言所给值 ```val``` 是否为目标值中的一个。
```
expect(new Map([['a', 1], ['b', 2]])).to.include(2);
```

由于 ```.include``` 根据目标类型有不同行为，在使用前检测目标类型十分必要。
```
expect([1, 2, 3]).to.be.an('array').that.includes(2);
```

默认情况下，使用严格相等（===）比较数组成员和对象属性。在之前添加 ```.deep``` 可以使用深度相等。
```
// Target array deeply (but not strictly) includes `{a: 1}`
expect([{a: 1}]).to.deep.include({a: 1});
expect([{a: 1}]).to.not.include({a: 1});

// Target object deeply (but not strictly) includes `x: {a: 1}`
expect({x: {a: 1}}).to.deep.include({x: {a: 1}});
expect({x: {a: 1}}).to.not.include({x: {a: 1}});
```

默认情况下，当目标为对象时会搜索目标所有属性包括继承属性及不可枚举属性。在之前添加 ```.own``` 会排除对继承属性的搜索。
```
Object.prototype.b = 2;

expect({a: 1}).to.own.include({a: 1});
expect({a: 1}).to.include({b: 2}).but.not.own.include({b: 2});
```
```.deep``` 和 ```.own``` 可以联合使用
```
expect({a: {b: 2}}).to.deep.own.include({a: {b: 2}});
```

在 ```include``` 之前添加 ```.nested``` 可以使用点中括号记号法引用嵌套属性。
```
expect({a: {b: ['x', 'y']}}).to.nested.include({'a.b[1]': 'y'});
```

如果，```.``` 或 ```[]``` 属性名的一部分，可以通过在之前添加添加两个反斜杠进行转译：
```
expect({'.a': {'[b]': 'x'}}).to.have.nested.property('\\.a.\\[b\\]');
expect({'.a': {'[b]': 'x'}}).to.nested.include({'\\.a.\\[b\\]': 'x'});
```

```.deep``` 和 ```.nested``` 能够联合使用。
```
expect({a: {b: [{c: 3}]}}).to.deep.nested.include({'a.b[0]': {c: 3}});
```
```.own``` 与 ```.nested``` 不能联合使用。

在前面添加 ```.not``` 否定 ```.include```。
```
expect('foobar').to.not.include('taco');
expect([1, 2, 3]).to.not.include(4);
```

然而当目标是一个对象时否定 ```.include``` 是存在风险的。断言目标对象不完全包含所给键值对但可能有包含部分所给键值对。

当不期望目标对象拥有 ```val``` 的中 keys 时，最好使用：
```
expect({c: 3}).to.not.have.any.keys('a', 'b'); // Recommended
expect({c: 3}).to.not.include({a: 1, b: 2}); // Not recommended
```
当期望目标对象含有所给 ```val``` keys 时，最好断言每个属性拥有期望值，而不是断言每个属性不含有众多不期望值中的一个。
```
expect({a: 3, b: 4}).to.include({a: 3, b: 4}); // Recommended
expect({a: 3, b: 4}).to.not.include({a: 1, b: 2}); // Not recommended
```

```.include``` 接受一个可选参数 ```msg```，该参数是一条断言失败时展示的自定义错误消息。这条消息也可以作为 ```expect``` 的第二个参数。
```
expect([1, 2, 3]).to.include(4, 'nooo why fail??');
expect([1, 2, 3], 'nooo why fail??').to.include(4);
```

```.include``` 可以作为语言链中的一个环节，在它之后的 ```.members``` 和 ```.keys``` 断言要求目标集合是期望集合的超集，而不必是完全相同的集合。注意当在 ```.members``` 前使用 ```.include``` 后，```.members``` 会忽略重复部分。
```
// Target object's keys are a superset of ['a', 'b'] but not identical
expect({a: 1, b: 2, c: 3}).to.include.all.keys('a', 'b');
expect({a: 1, b: 2, c: 3}).to.not.have.all.keys('a', 'b');

// Target array is a superset of [1, 2] but not identical
expect([1, 2, 3]).to.include.members([1, 2]);
expect([1, 2, 3]).to.not.have.members([1, 2]);

// Duplicates in the subset are ignored
expect([1, 2, 3]).to.include.members([1, 2, 2, 2]);
```
注意在断言链中 ```.include``` 之前添加 ```.any``` 会使 ```.keys``` 忽略 ```.include```。
```
// Both assertions are identical
expect({a: 1}).to.include.any.keys('a', 'b');
expect({a: 1}).to.have.any.keys('a', 'b');
```
```.contain```, and ```.contains``` 作为 ```.include``` 的别名可以相互替换。

### .ok

断言目标 宽松等于（==） ```true``` 。但是，最好使用严格等于（===）或深度等于期望值。
```
expect(1).to.equal(1); // Recommended
expect(1).to.be.ok; // Not recommended

expect(true).to.be.true; // Recommended
expect(true).to.be.ok; // Not recommended
```

使用 ```.not``` 否定 ```.ok```。
```
expect(0).to.equal(0); // Recommended
expect(0).to.not.be.ok; // Not recommended

expect(false).to.be.false; // Recommended
expect(false).to.not.be.ok; // Not recommended

expect(null).to.be.null; // Recommended
expect(null).to.not.be.ok; // Not recommended

expect(undefined).to.be.undefined; // Recommended
expect(undefined).to.not.be.ok; // Not recommended
```
自定义错误消息可以作为 ```expect``` 的第二参数。
```
expect(false, 'nooo why fail??').to.be.ok;
```

### .true

断言目标是否严格等于 ```true```。
```
expect(true).to.be.true;
```
可以通过 ```.not``` 进行否定。最好断言目标等于期望值，而不是不等于 ```true```。
```
expect(false).to.be.false; // Recommended
expect(false).to.not.be.true; // Not recommended

expect(1).to.equal(1); // Recommended
expect(1).to.not.be.true; // Not recommended
```
自定义错误消息可以作为 ```expect``` 的第二参数。
```
expect(false, 'nooo why fail??').to.be.true;
```

### .false

断言目标是否严格等于 ```false```。
```
expect(true).to.be.false;
```
可以通过 ```.not``` 进行否定。最好断言目标等于期望值，而不是不等于 ```false```。
```
expect(false).to.be.true; // Recommended
expect(false).to.not.be.false; // Not recommended

expect(1).to.equal(1); // Recommended
expect(1).to.not.be.false; // Not recommended
```
自定义错误消息可以作为 ```expect``` 的第二参数。
```
expect(true, 'nooo why fail??').to.be.false;
```

### .null

断言目标是否严格等于 ```null```。
```
expect(true).to.be.null;
```
可以通过 ```.not``` 进行否定。最好断言目标等于期望值，而不是不等于 ```null```。
```
expect(1).to.equal(1); // Recommended
expect(1).to.not.be.null; // Not recommended
```
自定义错误消息可以作为 ```expect``` 的第二参数。
```
expect(42, 'nooo why fail??').to.be.null
```

### .undefined

断言目标是否严格等于 ```undefined```。
```
expect(true).to.be.undefined;
```
可以通过 ```.not``` 进行否定。最好断言目标等于期望值，而不是不等于 ```undefined```。
```
expect(1).to.equal(1); // Recommended
expect(1).to.not.be.undefined; // Not recommended
```
自定义错误消息可以作为 ```expect``` 的第二参数。
```
expect(42, 'nooo why fail??').to.be.undefined;
```

### .NaN

断言目标是否严格等于 ```NaN```。
```
expect(true).to.be.NaN;
```
可以通过 ```.not``` 进行否定。最好断言目标等于期望值，而不是不等于 ```undefined```。
```
expect('foo').to.equal('foo'); // Recommended
expect('foo').to.not.be.NaN; // Not recommended
```
自定义错误消息可以作为 ```expect``` 的第二参数。
```
expect(42, 'nooo why fail??').to.be.NaN;
```

### .exist

断言目标是否严格不等于 ```null`` 或 ```undefined```。最好是断言目标等于期望值。
```
expect(1).to.equal(1); // Recommended
expect(1).to.exist; // Not recommended

expect(0).to.equal(0); // Recommended
expect(0).to.exist; // Not recommended
```
使用 ```.not``` 否定 ```.exist```。
```
expect(null).to.be.null; // Recommended
expect(null).to.not.exist; // Not recommended

expect(undefined).to.be.undefined; // Recommended
expect(undefined).to.not.exist; // Not recommended
```
自定义错误消息可以作为 ```expect``` 的第二参数。
```
expect(null, 'nooo why fail??').to.exist;
```

### .empty

当判定对象为字符串或数组时，```.empty``` 断言目标 ```length``` 属性是否严格等于（===）0。
```
expect([]).to.be.empty;
expect('').to.be.empty;
```

当目标是 map 或 set 时，```.empty``` 断言目标 ```size``` 属性是否严格等于（===）0。
```
expect(new Set()).to.be.empty;
expect(new Map()).to.be.empty;
```

当目标是一个非函数对象时，```.empty``` 断言对象是否拥有可枚举非继承属性。Symbol-based 类属性不计在内。
```
expect({}).to.be.empty;
```

由于 ```.empty``` 会根据不同的类型产生不同行为，所以在使用前确定目标类型十分重要。
```
expect([]).to.be.an('array').that.is.empty;
```

使用 ```.not``` 否定 ```.empty```。然而最好断言目标包含的值的数量，而不是断言它是否为空。
```
expect([1, 2, 3]).to.have.lengthOf(3); // Recommended
expect([1, 2, 3]).to.not.be.empty; // Not recommended

expect(new Set([1, 2, 3])).to.have.property('size', 3); // Recommended
expect(new Set([1, 2, 3])).to.not.be.empty; // Not recommended

expect(Object.keys({a: 1})).to.have.lengthOf(1); // Recommended
expect({a: 1}).to.not.be.empty; // Not recommended
```

自定义错误消息可以作为 ```expect``` 的第二参数。
```
expect([1, 2, 3], 'nooo why fail??').to.be.empty;
```

### .arguments

断言目标是一个 ```arguments``` 对象。
```
function test () {
  expect(arguments).to.be.arguments;
}

test();
```
可以使用 ```.not``` 否定判断。然而，最好断言目标为期望类型，而不是断言目标不是 ```arguments```。
```
expect('foo').to.be.a('string'); // Recommended
expect('foo').to.not.be.arguments; // Not recommended
```
自定义错误消息可以作为 ```expect``` 的第二参数。
```
expect({}, 'nooo why fail??').to.be.arguments;
```

作为别名 ```.Arguments``` 可以替换 ```.arguments```。

### .equal(val[, msg])

+ @param { Mixed } val
+ @param { String } msg _optional_

判断目标是否严格等于（===）给定值 ```val```。
```
expect(1).to.equal(1);
expect('foo').to.equal('foo');
```
使用 ```.deep``` 后表示深度等于（==）。
```
// Target object deeply (but not strictly) equals `{a: 1}`
expect({a: 1}).to.deep.equal({a: 1});
expect({a: 1}).to.not.equal({a: 1});

// Target array deeply (but not strictly) equals `[1, 2]`
expect([1, 2]).to.deep.equal([1, 2]);
expect([1, 2]).to.not.equal([1, 2]);
```

使用 ```.not``` 进行否定断言。最好断言目标等于它的期望值，而不是断言不等于众多不期望值中的一个。
```
expect(1).to.equal(1); // Recommended
expect(1).to.not.equal(2); // Not recommended
```
```.equal``` 接受可选参数 ```msg``` 用于断言失败时展示消息。
```
expect(1).to.equal(2, 'nooo why fail??');
expect(1, 'nooo why fail??').to.equal(2);
```
作为别名 ```.eq``` 可以替换 ```.equal```。

### .eql(obj[, msg])

+ @param { Mixed } obj
+ @param { String } msg _optional_

断言目标是否深度等于所给对象 ```obj```。
```
// Target object is deeply (but not strictly) equal to {a: 1}
expect({a: 1}).to.eql({a: 1}).but.not.equal({a: 1});

// Target array is deeply (but not strictly) equal to [1, 2]
expect([1, 2]).to.eql([1, 2]).but.not.equal([1, 2]);
```

使用 ```.not``` 进行否定断言。最好断言目标等于它的期望值，而不是断言不等于众多不期望值中的一个。
```
expect({a: 1}).to.eql({a: 1}); // Recommended
expect({a: 1}).to.not.eql({b: 2}); // Not recommended
```

```.equal``` 接受可选参数 ```msg``` 用于断言失败时展示消息。
```
expect({a: 1}).to.eql({b: 2}, 'nooo why fail??');
expect({a: 1}, 'nooo why fail??').to.eql({b: 2});
```

```.eqls``` 可与 ```.eql``` 相互替换。

```.deep.equal``` 基本等同于 ```.eql``` 但有一点不同：```.deep.equal``` 会引起位于其后的其他断言也采用深度比较。
```
expect({a: 1}).to.deep.equal({a: 1}).but.not.equal({a: 1});
```

### .above(n[, msg])

+ @param { Number } n
+ @param { String } msg _optional_

判定 number 或 date 类型的目标是否大于给定 number 或 date。然而尽可能的去判断目标是否等于期望值。
```
expect(2).to.equal(2); // Recommended
expect(2).to.be.above(1); // Not recommended
```

在之前添加 ```.lengthOf``` 来判定目标的 ```length``` 属性是否大于所给值 ```n```。
```
expect('foo').to.have.lengthOf(3); // Recommended
expect('foo').to.have.lengthOf.above(2); // Not recommended

expect([1, 2, 3]).to.have.lengthOf(3); // Recommended
expect([1, 2, 3]).to.have.lengthOf.above(2); // Not recommended
```

使用 ```.not``` 进行否定。
```
expect(2).to.equal(2); // Recommended
expect(1).to.not.be.above(2); // Not recommended
```

```.above``` 接受可选参数 ```msg``` 用于断言失败时展示消息。
```
expect(1).to.be.above(2, 'nooo why fail??');
expect(1, 'nooo why fail??').to.be.above(2);
```

```.gt``` 和 ```.greatThan``` 为 ```.above``` 的别名。

### .least(n[, msg])

+ @param { Number } n
+ @param { String } msg _optional_

判定 number 或 date 类型的目标是否大于等于给定 number 或 date。然而尽可能的去判断目标是否等于期望值。
```
expect(2).to.equal(2); // Recommended
expect(2).to.be.at.least(1); // Not recommended
expect(2).to.be.at.least(2); // Not recommended
```

在之前添加 ```.lengthOf``` 来判定目标的 ```length``` 属性是否大于等于所给值 ```n```。
```
expect('foo').to.have.lengthOf(3); // Recommended
expect('foo').to.have.lengthOf.at.least(2); // Not recommended

expect([1, 2, 3]).to.have.lengthOf(3); // Recommended
expect([1, 2, 3]).to.have.lengthOf.at.least(2); // Not recommended
```

使用 ```.not``` 进行否定。
```
expect(1).to.equal(1); // Recommended
expect(1).to.not.be.at.least(2); // Not recommended
```

```.least``` 接受可选参数 ```msg``` 用于断言失败时展示消息。
```
expect(1).to.be.at.least(2, 'nooo why fail??');
expect(1, 'nooo why fail??').to.be.at.least(2);
```

```.gte``` 为 ```.least``` 的别名。