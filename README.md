`gulp-jspm` wraps the `jspm bundle moduleName` command line.

### Usage

The following code snippets are implemented at [demo/gulpfile.js](demo/gulpfile.js).

```js
var gulp = require('gulp');
var gulp_jspm = require('gulp-jspm'); // npm install gulp-jspm

gulp.task('default', function(){
    return gulp.src('src/main.js')
        .pipe(gulp_jspm())
        .pipe(gulp.dest('build/'));
});
```

This will generate the `demo/build/jspm-bundle.js` file.
This file corresponds to the file generated by the command `jspm bundle main`.


###### Source Map

```js
var sourcemaps = require('gulp-sourcemaps');

gulp.src('src/main.js')
    .pipe(sourcemaps.init())
    .pipe(gulp_jspm())
    .pipe(sourcemaps.write('.'))
    .pipe(gulp.dest('build/'));
```

###### Original Entry Point

```js
gulp.src('src/main.js')
    .pipe(gulp_jspm())
    .pipe(pass(function(vinyl_file){
        assert( vinyl_file.relative === 'jspm-bundle.js' );
        assert( vinyl_file.original_entry_point.relative === 'main.js' );
    }));
```

###### jspm bunlde arithmetics

```js
gulp.src('src/main.js')
    .pipe(gulp_jspm({arithmetic: '- message'})) // excludes message.js from bundle
    .pipe(gulp.dest('build/'));
```

###### Self Executing Bundle

```js
gulp.src('src/main.js')
    .pipe(gulp_jspm({selfExecutingBundle: true})) // corresponds to `jspm bundle-sfx main`
    .pipe(gulp.dest('build/'));
```

##### Run Gulpfile Demo

To run the code snippets above execute following commands.

```js
git clone git@github.com:brillout/gulp-jspm
cd gulp-jspm/
npm install
cd demo/
npm install
npm install -g gulp
gulp
gulp sourcemap
gulp test
```

