## `gulp3`

### 1. 下载`node`

### 2. 安装`cnpm`

### 3. `gulp`官网

### 4. 安装`gulp`

- 用`cnpm`安装全局`gulp`

### 5. `package.json`

- 在项目根目录下

- 如果手动新建这个文件，而且这个文件里面的文本时空的就会报出以下

  ```js
  // Unexpected end of JSON input
  // JSON输入意外结束
  ```

- 这个文件时在你输入`cnpm init`或者`cnpm init -y`之后自动生成的

### 6. 初始化项目

```js
// 询问步骤
cnpm init
// 默认
cnpm init -y
```

### 7.本地`gulp`

```js
cnpm install --save-dev gulp@3
// 要安装gulp的3版本，最新版本是4
```

### 8. `html`

```js
const gulp = require('gulp');
gulp.task('html', function() {
  return gulp.src('src/*.html')
  .pipe(gulp.dest('dist/'))
});
```

### 9.`css`

```js
// cnpm install node-sass gulp-sass --save-dev
// cnpm install --save-dev gulp-autoprefixer
const sass = require('gulp-sass');
sass.compiler = require('node-sass');
const autoprefixer = require('gulp-autoprefixer');

gulp.task('css', function() {
  return gulp.src('src/sass/*.scss')
    .pipe(autoprefixer(['last 2 versions', 'Android >= 4.0'],))
    // 嵌套输出方式 nested
    // 展开输出方式 expanded 
    // 紧凑输出方式 compact 
    // 压缩输出方式 compressed
    .pipe(sass(
      {outputStyle: 'expanded'}
    ).on('error', sass.logError))
    .pipe(gulp.dest('dist/css/'))
});
// 如果html里面样式没有变化，可能是没有引入css文件
// 如果修改outputStyle没变化，看复制的对不对
```

### 10. `js`

```js
// cnpm install --save-dev gulp-babel@7 babel-core babel-preset-es2015
const babel = require("gulp-babel");
gulp.task('js', function() {
  return gulp.src('src/js/*.js')
  .pipe(babel({
    presets: ['es2015']
  }))
  .pipe(gulp.dest('dist/js'))
});
// gulp-babel要装7.0.1版本
// 要安装 babel-preset-es2015
```

### 11.自动更新

```js
// cnpm install --save-dev gulp-connect
// cnpm install --save-dev gulp-livereload
// cnpm install open --save-dev
// cnpm install --save-dev gulp-watch
const connect = require('gulp-connect');
const livereload = require('gulp-livereload');
const open = require('open');
gulp.task('default', ['html', 'css', 'js'], function() {
  livereload.listen();
  connect.server({
    root: 'dist',
    port: 5000,
    livereload: true
  });
  open('http://localhost:5000');
  gulp.watch('./src/*.html', ['html']);
  gulp.watch('src/sass/*.scss', ['css']);
  gulp.watch('src/js/*.js', ['js']);
});
// 安装 gulp-connect
// 如果报错，可能是 gulp-livereload 和 gulp版本是4.0.2
// 旧版gulp是安装 3.9.1
// 如果没有自动更新，可能是该任务没有写 .pipe(livereload());
// 如果样式或者js代码没有变化，可能是没有引入
```


