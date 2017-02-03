# GulpExpress
Configuration for a Node Server and Express with Gulp

Necessary:
Make sure you have installed Node.

Create a file with name: <strong>'package.json'</strong>:

<pre>

{
  "name": "YourNameApp",
  "version": "0.0.0",
  "description": "YourDescription",
  "main": "app.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": {
    "name": "YourName",
    "email": "xxxx@wxxxxxx.net",
    "url": "YourWeb"
  },
  "license": "MIT",
  "dependencies": {
    "express": "^4.8.2"
  },
  "devDependencies": {
    "browser-sync": "^1.3.3",
    "gulp": "^3.8.7",
    "gulp-nodemon": "^1.0.4"
  }
}
</pre>

Create a file with name: <strong> 'app.js'</strong>
<pre>
'use strict';
// simple express server
var express = require('express');
var app = express();
var router = express.Router();
app.use(express.static('public'));
app.get('/', function(req, res) {
    res.sendfile('./public/index.html');
});
app.listen(9999);

</pre>

Create a file with name: <strong>'gulpfile.js'</strong>
<pre>
'use strict';
var gulp = require('gulp');
var browserSync = require('browser-sync');
var nodemon = require('gulp-nodemon');
gulp.task('default', ['browser-sync'], function () {
});
gulp.task('browser-sync', ['nodemon'], function() {
	browserSync.init(null, {
		proxy: "http://localhost:9999",
        files: ["public/**/*.*"],
        browser: "google chrome",
        port: 8888,
	});
});
gulp.task('nodemon', function (cb) {
var started = false;
return nodemon({
		script: 'app.js'
	}).on('start', function () {
		// to avoid nodemon being started multiple times
		// thanks @matthisk
		if (!started) {
			cb();
			started = true; 
		} 
	});
});

</pre>

Create a folder with name: <strong>'public'</strong> in same directory.

Installing node dipendencies with the terminal Window/Mac/linux with the command <strong>'npm install'</strong>

Start the servers (Node and Express) with <strong>gulp default</strong> command.

Open the browser (if not open) to : <strong>'http://localhost:8888'</strong>






