## `gulp`

### 1. 下载`node`

### 2. 安装`cnpm`

### 3. `gulp`官网

### 4. 安装`gulp`

- 用`cnpm`安装全局`gulp`

### 5. 初始化项目

```js
// 询问
cnpm init
// 默认
cnpm init -y
```

### 6.本地`gulp`

```js
cnpm install --save-dev gulp
```

### 7. `html`

```js
gulp.task('html', function() {
  return gulp.src('src/index.html')
  .pipe(gulp.dest('dist/'));
});
```

### 8.`css`

```js
gulp.task('css', function() {
  return gulp.src('src/sass/index.scss')
  .pipe(autoprefixer(['last 2 versions', 'Android >= 4.0'],))
  // 嵌套输出方式 nested
  // 展开输出方式 expanded 
  // 紧凑输出方式 compact 
  // 压缩输出方式 compressed
  .pipe(sass(
    {outputStyle: 'expanded'}
  ).on('error', sass.logError))
  .pipe(gulp.dest('dist/css/'));
});
```

### 9. `js`

```js
gulp.task('js', function() {
  return gulp.src('src/js/index.js')
  .pipe(babel({
    presets: ['es2015']
  }))
  .pipe(gulp.dest('dist/js'));
});
// 报错 babel-core 没安装
// 要安装 babel-preset-es2015
```

### 10.自动更新

```js
gulp.task('watch', ['html', 'css', 'js'], function() {
  livereload.listen();
  connect.server({
    root: 'dist',
    port: 8000,
    host: '192.168.0.123',
    livereload: true
  });
  open('192.168.0.123:8000');
  gulp.watch('./src/*.html', ['html']);
  gulp.watch('src/sass/*.scss', ['css']);
  gulp.watch('src/js/*.js', ['js']);
});
// 如果报错，可能是 gulp-livereload 和 gulp版本是4.0.2
// 旧版gulp是安装 3.9.1
```







