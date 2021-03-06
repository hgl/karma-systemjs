# karma-systemjs    [![Build Status](https://travis-ci.org/rolaveric/karma-systemjs.png?branch=master)](https://travis-ci.org/rolaveric/karma-systemjs)
[Karma](http://karma-runner.github.io/) plugin for using [SystemJS](https://github.com/systemjs/systemjs) as a module loader.

# Installation

karma-systemjs requires SystemJS and es6-module-loader to be installed.

`npm install karma-systemjs systemjs es6-module-loader`

If testing in PhantomJS, you must install phantomjs-polyfill, as SystemJS >= v0.16 uses `Function.prototype.bind()`.

`npm install phantomjs-polyfill`

If using a transpiler, be sure to install it too. Traceur and Babel are supported:

`npm install traceur`

`npm install babel`

# Karma Configuration

Add `karma-systemjs` to your list of plugins:

`plugins: ['karma-systemjs', ...]`

Add `systemjs` to your list of frameworks:

`frameworks: ['systemjs', ...]`

Add SystemJS configuration:

```js
systemjs: {
	// Path to your SystemJS configuration file
	configFile: 'app/system.conf.js',

	// File patterns for your application code, dependencies, and test suites
	files: [
		'app/bower_components/angular/angular.js',
		'app/bower_components/angular-route/angular-route.js',
		'app/bower_components/angular-mocks/angular-mocks.js',
		'app/*/**/*.js'
	],

	// SystemJS configuration specifically for tests, added after your config file.
	// Good for adding test libraries and mock modules
	config: {
		paths: {
			'angular-mocks': 'bower_components/angular-mocks/angular-mocks.js'
		}
	},

	// Specify the suffix used for test suite file names.  Defaults to .test.js, .spec.js, _test.js, and _spec.js
	testFileSuffix: '.spec.js'
}
```

Adding file patterns under `systemjs.files` saves you from specifying each file pattern as 'served' but not 'included'.

```js
// These are equivalent
files: [
	{pattern: 'app/**/*.js', served: true, included: false, watched: true}
],

systemjs: {
	files: [
		'app/**/*.js'
	]
}
```

karma-systemjs defaults to using Traceur as transpiler. To use Babel, add the following to the SystemJS configuration:

```js
systemjs: {
	config: {
		transpiler: 'babel'
	}
}
```

The transpiler can also be omitted by setting `transpiler` to `null`.

# Examples

* [angular-phonecat](https://github.com/rolaveric/angular-phonecat/tree/es6)
* [angular-seed](https://github.com/rolaveric/angular-seed/tree/es6)
* [ngBoilerplate](https://github.com/rolaveric/ngbp/tree/es6)
