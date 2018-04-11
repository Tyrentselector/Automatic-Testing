# 代码测试率覆盖报告

我们使用 [karma-coverage-istanbul-reporter](https://www.npmjs.com/package/karma-coverage-istanbul-reporter) 生成代码测试覆盖率报告：

# 简介

这个报告器并不会正检测我们的代码。babel 用户应该使用 [istanbul babel plugin ](https://github.com/istanbuljs/babel-plugin-istanbul) 来检测我们的代码，然后使用 karma reporter 生成报告。

# 安装

```
npm install --save-dev babel-plugin-istanbul
npm install karma-coverage-istanbul-reporter --save-dev
```

# 配置

## babel 配置

```
module: {
        rules: [
            {
                test: /\.js$/,
                use: {
                    loader: 'babel-loader',
                    options: {
                        plugins: ['istanbul']
                    }
                }
            }
        ]
    }
```

## reporter配置

```
// karma.conf.js
const path = require('path');
 
module.exports = function (config) {
 
  config.set({
 
    // ... rest of karma config
 
    // anything named karma-* is normally auto included so you probably dont need this
    plugins: ['karma-coverage-istanbul-reporter'],
 
    reporters: ['coverage-istanbul'],
 
    // any of these options are valid: https://github.com/istanbuljs/istanbuljs/blob/aae256fb8b9a3d19414dcf069c592e88712c32c6/packages/istanbul-api/lib/config.js#L33-L39
    coverageIstanbulReporter: {
 
      // reports can be any that are listed here: https://github.com/istanbuljs/istanbuljs/tree/aae256fb8b9a3d19414dcf069c592e88712c32c6/packages/istanbul-reports/lib
      reports: ['html', 'lcovonly', 'text-summary'],
 
      // base output directory. If you include %browser% in the path it will be replaced with the karma browser name
      dir: path.join(__dirname, 'coverage'),
 
      // Combines coverage information from multiple browsers into one report rather than outputting a report
      // for each browser.
      combineBrowserReports: true,
 
      // if using webpack and pre-loaders, work around webpack breaking the source path
      fixWebpackSourcePaths: true,
 
      // stop istanbul outputting messages like `File [${filename}] ignored, nothing could be mapped`
      skipFilesWithNoCoverage: true,
 
       // Most reporters accept additional config options. You can pass these through the `report-config` option
      'report-config': {
 
        // all options available at: https://github.com/istanbuljs/istanbuljs/blob/aae256fb8b9a3d19414dcf069c592e88712c32c6/packages/istanbul-reports/lib/html/index.js#L135-L137
        html: {
          // outputs the report in ./coverage/html
          subdir: 'html'
        }
 
      },
 
       // enforce percentage thresholds
       // anything under these percentages will cause karma to fail with an exit code of 1 if not running in watch mode
      thresholds: {
        emitWarning: false, // set to `true` to not fail the test command when thresholds are not met
        global: { // thresholds for all files
          statements: 100,
          lines: 100,
          branches: 100,
          functions: 100
        },
        each: { // thresholds per file
          statements: 100,
          lines: 100,
          branches: 100,
          functions: 100,
          overrides: {
            'baz/component/**/*.js': {
              statements: 98
            }
          }
        }
      }
 
    }
  });
}
```

