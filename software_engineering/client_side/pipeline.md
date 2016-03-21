# Build and Test Pipeline

## Based on
http://jaredtong.com/2016/01/08/how-to-set-up-mocha-chai-sinon-karma-browserify-istanbul-codecov/

## Dependencies
npm install --save-dev babel-preset-es2015 babelify browserify-istanbul karma karma-browserify karma-chrome-launcher karma-coverage karma-mocha karma-phantomjs-launcher karma-sinon karma-chai karma-mocha mocha phantomjs phantomjs-prebuilt karma-mocha-reporter browserify-istanbul isparta

## package.json
```json
{
"scripts": {
    "test": "./node_modules/karma/bin/karma start karma.conf.js"
  },
  "browser": {
    "jquery": "./node_modules/jquery/dist/jquery.js",
    "bootstrap": "./node_modules/bootstrap/dist/js/bootstrap.js"
  },
  "browserify-shim": {
    "jquery": "$",
    "bootstrap": {
      "exports": "bootstrap",
      "depends": [
        "jquery:$"
      ]
    }
  },
  "browserify": {
    "transform": [
      ["babelify", {
        "ignore": [
          "/node_modules/"
        ],
        "presets": [
          "es2015",
          "react"
        ]
      }],
      ["node-underscorify", {
        "requires": [
          {
            "variable": "_",
            "module": "underscore"
          }
        ]
      }],
      "browserify-shim",
      ["browserify-istanbul", {
        "instrumenterConfig": {
          "embedSource": true
        }
      }]
    ]
  },
}
```

## karma.config.js
```javascript
// Karma configuration
// Generated on Fri Mar 18 2016 12:49:31 GMT-0700 (PDT)

module.exports = function(config) {
  config.set({

    // base path that will be used to resolve all patterns (eg. files, exclude)
    basePath: '',


    // frameworks to use
    // available frameworks: https://npmjs.org/browse/keyword/karma-adapter
    frameworks: ['mocha', 'sinon', 'chai', 'browserify'],

    plugins: [
      'karma-phantomjs-launcher',
      'karma-mocha',
      'karma-sinon',
      'karma-chai',
      'karma-browserify',
      'karma-mocha-reporter',
      'karma-coverage'
    ],

    // list of files / patterns to load in the browser
    files: [
      'js/**/*.js',
      'js/**/*.jsx',
      'js-admin/**/*.js',
      'js-admin/**/*.jsx',
      'test/**/*-test.js*'
    ],


    // list of files to exclude
    exclude: [
    ],


    // preprocess matching files before serving them to the browser
    // available preprocessors: https://npmjs.org/browse/keyword/karma-preprocessor
    preprocessors: {
      'js/**/*.js': ['browserify'],
      'js/**/*.jsx': ['browserify'],
      'js-admin/**/*.js': ['browserify'],
      'js-admin/**/*.jsx': ['browserify'],
      'test/**/*-test.js*': ['browserify']
    },


    // test results reporter to use
    // possible values: 'dots', 'progress'
    // available reporters: https://npmjs.org/browse/keyword/karma-reporter
    reporters: ['progress', 'mocha', 'coverage'],


    // web server port
    port: 9876,


    // enable / disable colors in the output (reporters and logs)
    colors: true,


    // level of logging
    // possible values: config.LOG_DISABLE || config.LOG_ERROR || config.LOG_WARN || config.LOG_INFO || config.LOG_DEBUG
    logLevel: config.LOG_INFO,


    // enable / disable watching file and executing tests whenever any file changes
    autoWatch: true,


    // start these browsers
    // available browser launchers: https://npmjs.org/browse/keyword/karma-launcher
    browsers: ['chrome'],


    // Continuous Integration mode
    // if true, Karma captures browsers, runs the tests and exits
    singleRun: false,

    // Concurrency level
    // how many browser should be started simultaneous
    concurrency: Infinity,

    browserify: {
      debug: true
      // transform: [
      //   ['browserify-istanbul', {
      //     instrumenterConfig: {
      //       embedSource: true
      //     }
      //   }]
      // ]
      // transform: [
      //   ['babelify', {
      //     "ignore": [
      //       "/node_modules/"
      //     ],
      //     presets: ['es2015', 'react']
      //   }],
      //   ['node-underscorify', {
      //     'requires': [{
      //       'variable': '_',
      //       'module': 'undersore'
      //     }]
      //   }],
      //   'browserify-shim'
      // ]
    },

    coverageReporter: {
      reporters: [
        {'type': 'text'},
        {'type': 'html', dir: 'coverage'},
        {'type': 'lcov'}
      ]
    }
  });
}

```
