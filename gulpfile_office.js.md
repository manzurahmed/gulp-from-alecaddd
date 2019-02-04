# Office "gulpfile.js"

```js
var gulp = require('gulp');
// gulp-less
// https://www.npmjs.com/package/gulp-less
var less = require('gulp-less');
// gulp-rename
// npm install --save-dev gulp-rename
var rename = require( 'gulp-rename' );
// gulp css minify
// npm install --save-dev gulp-clean-css
let cleanCSS = require( 'gulp-clean-css' );
// Browserify
var browserify = require( 'browserify' );

// LESS AUTOPREFIX: less-plugin-autoprefix
// npm install --save-dev less-plugin-autoprefix
var LessAutoprefix = require('less-plugin-autoprefix');
var autoprefix = new LessAutoprefix({ browsers: ['last 2 versions'] });

// Minify + Uglify JavaScript with UglifyJS3.
// https://www.npmjs.com/package/gulp-uglif
var uglify = require( 'gulp-uglify' );

// LESS source file
//var styleSRC   = './less/template.less'; // source file
var styleSRC   = ['less/template.less','less/template-news.less','less/program.less'];
var styleDIST  = './assets/css/'; // destination path
var styleWatch = 'less/*.less';

var jsSRC = 'js/custom.js';
var jsDIST  = './assets/js/';
var jsWatch = 'js/*.js';
var jsFILES = [jsSRC]; // in the array, include your files to handle

// To run this task seperately: "gulp style"
gulp.task( 'style', function(){
    return gulp.src( styleSRC )
        // Compile .less file
        .pipe(
            less({
                plugins: [autoprefix]
            })
        )
        // minify the CSS file with IE8 compatibility
        .pipe( cleanCSS({compatibility: 'ie8'}) )
        // rename ".less" file as ".min.css" file
        .pipe(
            rename( {
                suffix: '.min',
                extname: ".css"
            } )
        )
        // save file in destination folder
        .pipe( gulp.dest( styleDIST ) );
});

gulp.task( 'js', function() {
    return gulp.src( jsSRC )
    .pipe( uglify() )
    .pipe(
        rename( {
            suffix: '.min',
            extname: ".js"
        } )
    )
    .pipe(
        gulp.dest( jsDIST )
    );
});

// default task: Just type "gulp" in the terminal and
// the tasks specified in "gulp.parallel" will be run.
gulp.task( 'default', 
    gulp.parallel('style', 'js')
);

// Setting Up Watch
gulp.task( 'watch', function() {
    // https://gulpjs.org/API.html#gulp-watch-globs-opts-fn
    // gulp.watch(globs[, opts][, fn])
    // globs = A path string, an array of path strings, a glob string or an array of glob strings
    // opts = delay, queue, ignoreInitial
    // fn = If the fn is passed, it will be called when the watcher emits a change, add or unlink event.
    gulp.watch( styleWatch, gulp.series('style') );
    gulp.watch( jsWatch, gulp.series('js') );
});
```
