# 可用浏览器加载器

* [Chrome and Chrome Canary](https://www.npmjs.com/package/karma-chrome-launcher)
* [Firefox](https://www.npmjs.com/package/karma-firefox-launcher)
* [Safari](https://www.npmjs.com/package/karma-safari-launcher)
* [PhantomJS](https://www.npmjs.com/package/karma-phantomjs-launcher)
* [JSDOM](https://www.npmjs.com/package/karma-jsdom-launcher)
* [Opera](https://www.npmjs.com/package/karma-opera-launcher)
* [Internet Explorer](https://www.npmjs.com/package/karma-ie-launcher)
* [SauceLabs](https://www.npmjs.com/package/karma-saucelabs-launcher)
* [BrowserStack](https://www.npmjs.com/package/karma-browserstack-launcher)
* [所有加载器](https://www.npmjs.com/browse/keyword/karma-launcher)

例如添加 Firefox 到测试套件中：
```
# 通过 Npm 安装加载器
$ npm install karma-firefox-launcher --save-dev
```
然后在你的配置文件 ```browsers``` 配置项数组中添加浏览器名称。
```
module.exports = function(config) {
  config.set({
    browsers : ['Chrome', 'Firefox']
  });
};
```
同时请注意，```browsers``` 选项默认为空数组。

更多细节参考[ Browsers 配置](browsers_option.md)