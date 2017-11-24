# 为什么需要Sinon
当我们在开发前端项目的时候, 很多时候需要根据后端返回的数据来渲染页面, 我们通常使用AJAX发送请求给服务端。当我们开发后端逻辑的时候有时候需要连接数据库,根据从数据库中得到的数据来执行后续的逻辑代码, 或者其他的依赖, 甚至会更加复杂棘手。这些开发都存在一个共同的局限性, 就是会去依赖别的服务, 需要别的系统的支持。 例如, 如果我们使用Ajax请求网络, 您需要有一个服务器来响应对应的请求。对于数据库, 您需要有一个为测试设置的测试数据库。

所有这些都意味着编写和运行测试更加困难, 因为您需要做额外的工作来准备和设置一个测试成功的环境。
值得庆幸的是, 我们可以用sinon.js避免所有麻烦。我们可以利用它的特性将上面的例子简化为几行代码。

然而, 第一次接触spies, stub, mock可能棘手。它可能很难选择什么时候用什么功能。它们也有一些问题，所以你需要知道你应该用什么功能解决什么样的问题。
在这篇文章中将向你展示spies, stub, mock何时以及如何使用它们，并给你一套最佳实践，帮助您避免常见的陷阱.

# 什么是Sinon
Sinon具有独立的spies, stub, mock功能,Sinon并不是独立的测试框架,它只是在测试中提供了上述的三种功能, 例如我们常用的测试框架Mocha,Sinon并不能完全替代Mocha的功能。

Sinon通过所谓的测试替代(test-double)轻松消除测试的复杂度,
测试替代，顾名思义，测试中用到的是真实代码逻辑的替代品。回过头来看Ajax示例，我们不需要设置服务器，而是用Ajax的替代代码，我们把Ajax的逻辑替换成不需要通过请求服务器就返回预先设置好的数据，这听起来有不可思议，但是基本概念很简单。因为JavaScript是动态的，所以我们可以在调用某个方法的时候使用任何函数来替换它。在Sinon中们可以用一个测试逻辑取代任何JavaScript函数，然后让测试复杂的事情变的简单化。