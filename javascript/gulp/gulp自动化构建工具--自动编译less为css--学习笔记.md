# [gulp自动化构建工具--自动编译less为css--学习笔记](http://www.cnblogs.com/CaktyRiven/p/6419674.html)

 1.安装

       命令：npm install gulp-less 或者 cnpm install gulp-less

 2.编写文件

 <a title="复制代码">![复制代码](http://common.cnblogs.com/images/copycode.gif)</a>

 //获取gulp
var gulp = require('gulp')

//获取gulp-less模块
```
var less = require("gulp-less")
```

//编译less
//在命令行输入gulp less启动此任务
```
gulp.task('less',function(){
    //1.找到less文件
    gulp.src('views/less/**.less')
    //2.编译为css
    .pipe(less())
    //3.另存为css
    .pipe(gulp.dest('views/dist1/css1'))
})

```
//在命令行gulp auto启动此任务
```
gulp.task('auto',function(){
    //监听文件修改，当文件修改则执行less任务
    gulp.watch('views/less/**.less',['less'])
})

```
//使用gulp.task('default')定义默认任务
//在命令行使用gulp启动images任务和auto任务
```
gulp.task('default',['less','auto'])

``` 
<a title="复制代码">![复制代码](http://common.cnblogs.com/images/copycode.gif)</a>

 3.执行
 
       gulp