---
title: gulp常用配置
date: 2019-10-24 22:51:31
tags: 前端
---

> 由于项目中经常会使用到gulp，而每次配置大概都差不多，所以将配置记录一下

### 项目结构

```
├─dist
│  ├─assets
│  ├─css
│  ├─images
│  └─js
├─node_modules
└─src
  ├─assets
  │  ├─css
  │  ├─echarts
  │  ├─js
  │  ├─odometer
  │  └─插件等
  ├─less
  ├─images
  └─js
```


### 配置文件 gulpfile.js

```
/*
 * @gulp：自动化任务
 */
var gulp = require('gulp');
var rm = require('del'); //删除文件
var browserSync = require('browser-sync');
var reload = browserSync.reload; //自动刷新
var htmlmin = require('gulp-htmlmin'); //压缩html
var miniCSS = require('gulp-clean-css'); //压缩css
var miniJS = require('gulp-uglify'); //压缩js
var less = require('gulp-less'); //编译less
var autoprefixer = require('gulp-autoprefixer'); // 补全浏览器前缀 
var babel = require('gulp-babel'); // es6 转 es5
var replace = require('gulp-replace'); // 替换
var proxyMiddleware = require('http-proxy-middleware'); // 代理跨域

/**
 * 配置
 */
var config = {
    path: {
        src: './src/', // 工程目录
        dist: './dist/' // 产出目录 
    },

    // 代理设置
    middleware: proxyMiddleware('/api', {
        target: 'http://192.168.1.108:8080',
        changeOrigin: true,
        pathRewrite: {
            '^/api': ''
        },
    })
};


/*清除产出目录*/
gulp.task('clear-dir', (done) => {
    rm.sync([config.path.dist + '**']);
    done();
});

/*图片产出*/
gulp.task('img', function () {
    return gulp.src(config.path.src + 'images/**/*')
        .pipe(gulp.dest(config.path.dist + 'images/'))
});

/**静态文件(不需要编译) */
gulp.task('assets', function () {
    return gulp.src(config.path.src + 'assets/**/*')
        .pipe(gulp.dest(config.path.dist + 'assets/'))
});


/**html处理 */
gulp.task('mini-html', function () {
    return gulp.src(config.path.src + '**.html')
        // 修改为源文件 
        //  .pipe(replace('src="./script/', 'src="./js/'))
        .pipe(htmlmin({
            collapseBooleanAttributes: true, //省略布尔属性的值 <input checked="true"/> ==> <input />
            removeEmptyAttributes: true, //删除所有空格作属性值 <input id="" /> ==> <input />
            removeScriptTypeAttributes: true, //删除<script>的type="text/javascript"
            removeStyleLinkTypeAttributes: true, //删除<style>和<link>的type="text/css"           
        }))
        .pipe(gulp.dest(config.path.dist))
         // 注入浏览器
         .pipe(reload({
            stream: true
        }));
});


/**less编译 */
gulp.task('less', function () {
    return (gulp.src(config.path.src + 'less/*.less')
        .pipe(less())
        // 补全前缀
        .pipe(autoprefixer({
            cascade: false, // 是否美化属性值 
            overrideBrowserslist: [
                'last 2 versions',
                'Chrome >= 25'
            ],
        }))
        .pipe(gulp.dest(config.path.dist + 'css/'))
        // 注入浏览器
        .pipe(reload({
            stream: true
        }))
    );
});

/**es6转es5 */
gulp.task('babel-js', function () {
    return gulp.src(config.path.src + 'js/**.js')
        .pipe(babel())
        .pipe(gulp.dest(config.path.dist + 'js/'))
        // 注入浏览器
        .pipe(reload({
            stream: true
        }));
});

/**开启服务 */
gulp.task('server', function () {
    browserSync.init({
        server: {
            baseDir: config.path.dist,
            index: 'index.html', // 指定默认打开的文件
            middleware: config.middleware
        },
        port:'8888',    // 默认3000 

    });
    /**监听 */
    // gulp.watch(config.path.src + '**.html').on('change', reload);
    gulp.watch(config.path.src + '**.html', gulp.series('mini-html'));
    gulp.watch(config.path.src + 'js/**.js', gulp.series('babel-js'));
    gulp.watch(config.path.src + 'less/**.less', gulp.series('less'));

});


/**
 * 开发：
 * 开启代理服务器，
 * 监听自动刷新,
 * es6转换
 * less编译补全前缀
 */
gulp.task('default', gulp.series('clear-dir','assets','img','mini-html', 'less', 'babel-js', 'server', (done) => {
    done();
}));


/**
 * 生产:
 * 合并，压缩等操作...
 */
```

