```
var gulp = require( 'gulp' );
var rename = require( 'gulp-rename' );
var sass = require(  'gulp-sass' );
var autoprefixer = require( 'gulp-autoprefixer' );
var sourcemaps = require( 'gulp-sourcemaps' );
var browserify = require( 'browserify' );
var babelify = require( 'babelify' );
var source = require( 'vinyl-source-stream' );
var buffer = require( 'vinyl-buffer' );
var uglify = require( 'gulp-uglify' );
var browserSync = require( 'browser-sync' ).create();
var reload = browserSync.reload;

// gulp is just dependent of tasks
var styleSRC = 'src/scss/style.scss';
var styleDIST = './dist/css/';
var styleWatch = 'src/scss/**/*.scss';

var jsSRC = 'script.js';
var jsFOLDER = 'src/js/';
var jsDIST = './dist/js/';
var jsWatch = 'src/js/**/*.js';
var jsFILES = [jsSRC];

var htmlWatch = '**/*.html';
var phpWatch = '**/*.php';

// Browser-sync - Video 7 Gulp
gulp.task('browser-sync', function(){
	browserSync.init({
		server: {
			baseDir: "./"
		},
		injectChanges: true
		// open: false,
		// injectChanges: true,
		// proxy: 'http://localhost/scsstest/',
		// https: {
		// 	key: '',
		// 	cert: ''
		// }
	});
});

gulp.task('style', function(){
	gulp.src( styleSRC )
		.pipe( sourcemaps.init() )
		.pipe( sass({
			errorLogToConsole: true,
			outputStyle: 'compressed'
		}) )
		.on( 'error', console.error.bind( console ) )
		.pipe( autoprefixer({
			browsers: ['last 2 versions'],
            cascade: false
		}) )
		.pipe( rename( { suffix: '.min' } ) )
		.pipe( sourcemaps.write( './' ) )
		.pipe( gulp.dest( styleDIST ) )
		.pipe( browserSync.stream() );
});

gulp.task('js', function(){
	jsFILES.map(function(entry){
		return browserify({
			entries: [jsFOLDER + entry]
		})
		.transform( babelify, { presets: ['env'] } )
		.bundle()
		.pipe( source( entry ) )
		.pipe( rename( { extname: '.min.js' }) )
		.pipe( buffer() )
		.pipe( sourcemaps.init({ loadMaps: true }) )
		.pipe( uglify() )
		.pipe( sourcemaps.write( './' ) )
		.pipe( gulp.dest( jsDIST ) )
		.pipe( browserSync.stream() );
	});

	// browserify (import modules, bundle apps and requires the script)
	// transform files with babelify (convert ES6 to regular vanila JS understandable by different browsers)
	// 		(babelify needs 2 more libraries, babel-core and babel-preset-env)
	// bundle all together
	// Source
	// Rename .min
	// Buffer
	// sourcemap
	// uglify
	// write sourcemap
	// save to distribute folder
	/*
	Note:
	1. "vinyl-source-stream" and "vinyl-buffer" works together. (Video Gulp 6 19:40)
	 */
});

gulp.task('default', ['style', 'js']);

gulp.task('watch', ['default', 'browser-sync'], function(){
	gulp.watch( styleWatch, ['style'] ); // NOTE: removed 'reload' from this line
	gulp.watch( jsWatch, ['js'], reload );
	gulp.watch( htmlWatch, reload );
	gulp.watch( phpWatch, reload );
});
```
