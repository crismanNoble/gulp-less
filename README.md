gulp-less
=========

A LESS plugin for Gulp

[![Build Status](https://travis-ci.org/plus3network/gulp-less.png?branch=master)](https://travis-ci.org/plus3network/gulp-less)

## Install

```
npm install gulp-less
```

## Usage
```javascript
var less = require('gulp-less');
var path = require('path');

gulp.task('less', function () {
  gulp.src('./less/**/*.less')
    .pipe(less({
      paths: [ path.join(__dirname, 'less', 'includes') ]
    }))
    .pipe(gulp.dest('./public/css'));
});
```


## Options

The options are the same as what's supported by the less parser, with the exception of `sourceMapFilename` and `sourcemap`.  These options will do nothing.  Use [gulp-sourcemaps](https://github.com/floridoo/gulp-sourcemaps) to generate sourcemaps.

## CleanCSS

As of version 1.3.7 of gulp-less, less 2.0 is being used. Cleancss has been removed from LESS core, and has become a less plugin. If you would like to continue to use cleancss, you need to use it as a LESS plugin.

```
npm install less-plugin-clean-css --save-dev
```

```javascript
var LessPluginCleanCSS = require("less-plugin-clean-css"),
    cleancss = new cleancssPlugin({advanced: true});

gulp.src('./less/**/*.less')
  .pipe(less({
    plugins: [cleancss]
  }))
  .pipe(gulp.dest('./public/css'));


```

See all options for cleancss here: https://github.com/jakubpawlowicz/clean-css#how-to-use-clean-css-programmatically

## Plugins

If you are using version 1.3.7 or higher you will have the ability to use a growing set LESS plugins, potentially simplifying your build steps.

Continuing on the cleancss as a plugin pattern, we can include the [autoprefix plugin](https://github.com/less/less-plugin-autoprefix).
```
npm install less-plugin-autoprefix --save-dev
```

```javascript
var LessPluginCleanCSS = require("less-plugin-clean-css"),
    cleancss = new cleancssPlugin({advanced: true});
    
var LessPluginAutoPrefix = require('less-plugin-autoprefix'),
    autoprefix= new LessPluginAutoPrefix({browsers: ["last 2 versions"]});


gulp.src('./less/**/*.less')
  .pipe(less({
    plugins: [autoprefix, cleancss]
  }))
  .pipe(gulp.dest('./public/css'));


```

More info on LESS plugins can be found at http://lesscss.org/usage/#plugins, including a current list of plugins.


## Source maps

gulp-less can be used in tandem with [gulp-sourcemaps](https://github.com/floridoo/gulp-sourcemaps) to generate source maps for the less to CSS transition. You will need to initialize [gulp-sourcemaps](https://github.com/floridoo/gulp-sourcemaps) prior to running the gulp-less compiler and write the source maps after.

```javascript
var sourcemaps = require('gulp-sourcemaps');

gulp.src('./less/**/*.less')
  .pipe(sourcemaps.init())
  .pipe(less())
  .pipe(sourcemaps.write())
  .pipe(gulp.dest('./public/css'));

// will write the source maps inline in the compiled CSS files
```

By default, [gulp-sourcemaps](https://github.com/floridoo/gulp-sourcemaps) writes the source maps inline in the compiled CSS files. To write them to a separate file, specify a relative file path in the `sourcemaps.write()` function.

```javascript
var sourcemaps = require('gulp-sourcemaps');

gulp.src('./less/**/*.less')
  .pipe(sourcemaps.init())
  .pipe(less())
  .pipe(sourcemaps.write('./maps'))
  .pipe(gulp.dest('./public/css'));

// will write the source maps to ./public/css/maps
```

## Error handling

By default, a gulp task will fail and all streams will halt when an error happens. To change this behavior check out the error handling documentation [here](https://github.com/gulpjs/gulp/blob/master/docs/recipes/combining-streams-to-handle-errors.md)

## License

(MIT License)

Copyright (c) 2014 Plus 3 Network dev@plus3network.com

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
