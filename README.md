# gulp-git-manifest
[![NPM version][npm-image]][npm-url] [![Build Status][travis-image]][travis-url] [![Dependency Status][depstat-image]][depstat-url]

> git-manifest plugin for [gulp](https://github.com/gulpjs/gulp)

## Usage

A plugin for Gulp to create a json manifest file with latest commit sha1 for each of the files in the project git-tree.

E.g. Use to create an artifact list for deployments. May be used as a basis for `gulp clean`, `gulp verify`, and `gulp patch` type tasks.

Whereas [gulp-rev](https://github.com/sindresorhus/gulp-rev) sets a hash based on content, this uses the sha1 hash from the latest git commit.

First, install `gulp-git-manifest` as a development dependency:

```shell
npm install --save-dev gulp-git-manifest
```

Then, add it to your `gulpfile.js`:

```javascript
var git-manifest = require("gulp-git-manifest");

var files = gulp.src("./src/*.ext")
	.pipe(git-manifest({
    length: 6,
    separator: "-"
  }))

files.on('data', function (file){
  console.log("Modified file:", file);
});
```

Full usage example:

```javascript
var git-manifest = require("gulp-git-manifest");

gulp.task('moveFiles'. function () {
  gulp.src("./src/*.ext")
     .pipe(git-manifest())
     .pipe(gulp.dest('./'));
});
```

## API

### git-manifest(options)

#### options.length
Type: `Integer`  
Default: 6

Length of the sha to show.

#### options.separator
Type: `String`  
Default: "-"

Separator before the suffix.

#### options.folder
Type: `Boolean`  
Default: "false"

If the sha-substring should be as a folder instead of suffix.
E.g.

```
New path:  /Code/gulp-git-manifest/test/fixtures/c03b75/a.txt
```


## Examples

To see all examples run from root:

```sh
$ gulp --gulpfile examples/gulpfile.js --tasks
[gulp] Using file /Users/example/gulp-git-manifest/examples/gulpfile.js
[gulp] Working directory changed to /Users/example/gulp-git-manifest/examples
[gulp] Tasks for /Users/example/gulp-git-manifest/examples/gulpfile.js
[gulp] ├── default
[gulp] ├── folder
[gulp] └── folderPrefix
```

Run example:

```sh
$ gulp --gulpfile examples/gulpfile.js
[gulp] Using file /Users/example/gulp-git-manifest/examples/gulpfile.js
[gulp] Working directory changed to /Users/example/gulp-git-manifest/examples
[gulp] Running 'default'...
[gulp] Finished 'default' in 4.43 ms
New path:  /Users/example/gulp-git-manifest/test/fixtures/a-eaa51c.txt
New path:  /Users/example/gulp-git-manifest/test/fixtures/b-eaa51c.txt
New path:  /Users/example/gulp-git-manifest/test/fixtures/c-eaa51c.txt
```

## Changelog
1.0.0:
 * Adds support for [`gulp-rev-replace`](https://github.com/jamesknelson/gulp-rev-replace)

0.2.0:
 * Adds possibility to have sha as subfolder instead of suffix

0.1.0:
 * Changes to using options object instead of two parameters on input.

0.0.4: 
 * No longer throws unjust error on streamed contents.

## License

[MIT License](http://en.wikipedia.org/wiki/MIT_License)

[npm-url]: https://npmjs.org/package/gulp-git-manifest
[npm-image]: https://badge.fury.io/js/gulp-git-manifest.png

[travis-url]: http://travis-ci.org/mikaelbr/gulp-git-manifest
[travis-image]: https://secure.travis-ci.org/mikaelbr/gulp-git-manifest.png?branch=master

[depstat-url]: https://david-dm.org/mikaelbr/gulp-git-manifest
[depstat-image]: https://david-dm.org/mikaelbr/gulp-git-manifest.png
