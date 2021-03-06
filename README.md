# gulp-data-contents [![NPM version](https://img.shields.io/npm/v/gulp-data-contents.svg?style=flat)](https://www.npmjs.com/package/gulp-data-contents) [![NPM monthly downloads](https://img.shields.io/npm/dm/gulp-data-contents.svg?style=flat)](https://npmjs.org/package/gulp-data-contents) [![NPM total downloads](https://img.shields.io/npm/dt/gulp-data-contents.svg?style=flat)](https://npmjs.org/package/gulp-data-contents) [![Linux Build Status](https://img.shields.io/travis/jonschlinkert/gulp-data-contents.svg?style=flat&label=Travis)](https://travis-ci.org/jonschlinkert/gulp-data-contents)

> Gulp plugin that replaces the contents of a file with the contents of another file using the filepath specified on the 'contents' property in front-matter. Customizable, useful for generating scaffolding or defining placeholder files.

## Install

Install with [npm](https://www.npmjs.com/):

```sh
$ npm install --save gulp-data-contents
```

## What does this do?

Given you have a file with the following [front-matter](https://github.com/jonschlinkert/gray-matter):

```
---
contents: scaffold.txt
---
```

This plugin will replace the contents of the file with the contents from `scaffold.txt`.

## Usage

```js
var gulp = require('gulp');
var contents = require('gulp-data-contents');

gulp.task('contents', function() {
  return gulp.src('example.txt')
    .pipe(contents())
    .pipe(gulp.dest('dist'));
});
```

## Options

### options.prop

Customize the file property to use. By default, `file.data.contents` is used.

**Type:**: `string`

**Default:**: `data.contents`

**Example**

```js
contents({prop: 'data.value'})
```

Which would be used like this:

```
---
value: scaffold.txt
---
```

Note that [gray-matter](https://github.com/jonschlinkert/gray-matter) (the front-matter parser used by [assemble](https://github.com/assemble/assemble), [metalsmith](https://github.com/segmentio/metalsmith), the [electron](https://github.com/electron-userland/electron-prebuilt) website and many others, uses the `file.data` property for front-matter. Other libraries might use a different property).

### options.cwd

Customize current working directory to use for filepath specified in front-matter. If not specified, `file.base` is used as the cwd.

**Type:**: `string`

**Default:**: `undefined`

**Example**

```js
contents({cwd: 'templates'})
```

### options.resolve

Custom function for resolving `file.contents` from the path defined in front-matter.

**Type:**: `function`

**Default:** Uses `fs.readFileSync()`

**Example**

```js
contents({
  resolve: function(file, options, next) {
    var fp = path.join('some/path', file.data.contents);
    file.contents = fs.readFileSync(fp);
    next(null, file);
  }
})
```

## About

### Contributing

Pull requests and stars are always welcome. For bugs and feature requests, [please create an issue](../../issues/new).

Please read the [contributing guide](.github/contributing.md) for advice on opening issues, pull requests, and coding standards.

### Building docs

_(This project's readme.md is generated by [verb](https://github.com/verbose/verb-generate-readme), please don't edit the readme directly. Any changes to the readme must be made in the [.verb.md](.verb.md) readme template.)_

To generate the readme, run the following command:

```sh
$ npm install -g verbose/verb#dev verb-generate-readme && verb
```

### Running tests

Running and reviewing unit tests is a great way to get familiarized with a library and its API. You can install dependencies and run tests with the following command:

```sh
$ npm install && npm test
```

### Author

**Jon Schlinkert**

* [github/jonschlinkert](https://github.com/jonschlinkert)
* [twitter/jonschlinkert](https://twitter.com/jonschlinkert)

### License

Copyright © 2017, [Jon Schlinkert](https://github.com/jonschlinkert).
Released under the [MIT License](LICENSE).

***

_This file was generated by [verb-generate-readme](https://github.com/verbose/verb-generate-readme), v0.6.0, on August 07, 2017._