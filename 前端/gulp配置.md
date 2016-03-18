## angular2项目的gulp配置
### 问题描述
#### 我想要将ｎｐｍ安装的ａｎｇｕｌａｒ２等等依赖项目移到ｌｉｂｓ的文件夹，同时插入到index.html


### 解决方案
#### 先将将依赖的项目从node_module文件夹中拷贝到libs文件夹中同时创建该文件夹
##### *定义路径*
```
exports.PATH = {
  dest: {
    all: '.tmp',
    dev: {
      all: 'serve',
      lib: 'serve/lib',
      ng2: 'serve/lib/angular2.js',
      router: 'serve/lib/router.js'
    },
    prod: {
      all: 'dist/prod',
      lib: 'dist/prod/lib'
    }
  },
  src: {
    // Order is quite important here for the HTML tag injection.
    baseLibs: [
      'node_modules/systemjs/dist/system-polyfills.js',
      'node_modules/systemjs/dist/system.js',
      'node_modules/systemjs/dist/system.src.js',
      'node_modules/es6-shim/es6-shim.js',
      'node_modules/rxjs/bundles/Rx.js',
      'node_modules/angular2/bundles/angular2-polyfills.js',
      'node_modules/angular2/bundles/angular2.js',
      'node_modules/angular2/bundles/router.js',
      'node_modules/angular2/bundles/http.js',
      'node_modules/angular2/bundles/upgrade.js',
      'node_modules/lodash/index.js',
      'node_modules/zone.js/dist/zone.js'
    ]
  }
};
```
##### *执行拷贝创建任务*
```
'use strict';

var gulp = require('gulp'),
    plugins = require('gulp-load-plugins')();
var conf = require('./conf');
gulp.task('merge', ['clean'], function () {
    return gulp.src(conf.PATH.src.baseLibs)
        .pipe(gulp.dest('.tmp/serve/libs/'))
});
```
##### 插入ｉｎｄｅｘ.ｈｔｍｌ
>1,先要将引用的ｊｓ文件前的路径全部清除，附上新的路径
```    
var libs = conf.PATH.src.baseLibs.map(function (paths) {
           return path.join('.tmp/serve/libs/', paths.split('/').pop());
       });
```
>2,进入该路径
```
   var injectlibs = gulp.src(libs, {read: false});
    var injectOptions = {
        ignorePath: [conf.paths.src, path.join(conf.paths.tmp, '/serve')],
        addRootSlash: false
    };
```
>3,执行插入
```
  return gulp.src(path.join(conf.paths.src, '/*.html'))
        .pipe($.inject(injectStyles, injectOptions))
        .pipe($.inject(injectScripts, injectOptions))
        .pipe($.inject(injectlibs, injectOptions))
        .pipe(wiredep(_.extend({}, conf.wiredep)))
        .pipe(gulp.dest(path.join(conf.paths.tmp, '/serve')));
```