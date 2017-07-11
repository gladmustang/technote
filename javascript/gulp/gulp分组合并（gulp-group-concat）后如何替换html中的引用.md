 

# [gulp分组合并（gulp-group-concat）后如何替换html中的引用？](https://segmentfault.com/q/1010000003908091)

*   [gulp](https://segmentfault.com/t/gulp)

 [**wtmanutd**](https://segmentfault.com/u/wtmanutd) 2015年10月26日提问 · [2015年10月26日更新](https://segmentfault.com/q/1010000003908091/revision)

*   关注 **12** 关注
*   收藏 **9** 收藏，**5.9k** 浏览

 问题对人有帮助，内容完整，我也想知道答案1问题没有实际价值，缺少关键内容，没有改进余地

现在需要对一个老的前端项目使用gulp进行合并打包等工作，
因为页面以及JS/CSS文件都很多，所以想使用gulp-group-concat进行分组合并后再根据mapping关系去替换原HTML中的引用，比如`plugins/a.js`，`plugins/b.js`，`plugins/b.js`合并为了`plugins/abc.js`, 则将HTML中所有引用到这三个文件的地方替换为`abc.js`（同时还要去重）

请问是否有插件能够实现以上需求？或者是否有更好的方案？

update =======
有两位朋友提到了gulp-useref和gulp-usemin，这两个插件之前也看过，感觉不是特别适用（也可能是我对用法还不够了解）。
我的理解是，这两个插件都是通过在html中写注释的方式定义我要怎么去合并js文件
但是，由于我在多个页面可能引用类似的js文件，
比如在`index.html`中引用了`a.js`, `b.js`, `c.js`，而`demo.html`中引用了`a.js`, `b.js`，我现在希望将`a.js`, `b.js`, `c.js`合并为`abc.js`，并同时对`index.html`和`demo.html`中的引用进行替换，替换后`index.html`和`demo.html`都只需要引用`abc.js`即可
这种场景不知道要怎么处理？

[https://github.com/jonkemp/gulp-useref/issues/140](https://github.com/jonkemp/gulp-useref/issues/140)
这个gulp-useref的issue跟我的问题类似，目前也尚未解决

*   [2015年10月26日提问](https://segmentfault.com/q/1010000003908091)
*   <a class="comments" data-id="1010000003908091" data-target="#comment-1010000003908091">3 评论</a>
*   <a data-title="gulp分组合并（gulp-group-concat）后如何替换html中的引用？" data-url="http://sfau.lt/bNqyPT" data-id="1010000003908091">邀请回答</a>
*   <a>编辑</a>

 [默认排序](https://segmentfault.com/q/1010000003908091#answers-title)[时间排序](https://segmentfault.com/q/1010000003908091?sort=created#answers-title)

## 5个回答

 答案对人有帮助，有参考价值1答案没帮助，是错误的答案，答非所问

发现一个插件应该适用你这种情况： [https://github.com/cgross/gulp-dom-src](https://github.com/cgross/gulp-dom-src)
贴一段官方的代码片段给你:

<code class="js">var gulp = require('gulp');
var domSrc = require('gulp-dom-src');
var concat = require('gulp-concat');
var cssmin = require('gulp-cssmin');
var uglify = require('gulp-uglify');
var cheerio = require('gulp-cheerio');

gulp.task('css', function() {
    return domSrc({file:'index.html',selector:'link',attribute:'href'})
        .pipe(concat('app.full.min.css'))
        .pipe(cssmin())
        .pipe(gulp.dest('dist/'));
});

gulp.task('js', function() {
    return domSrc({file:'index.html',selector:'script',attribute:'src'})
        .pipe(concat('app.full.min.js'))
        .pipe(uglify())
        .pipe(gulp.dest('dist/'));
});

gulp.task('indexHtml', function() {
    return gulp.src('index.html')
        .pipe(cheerio(function ($) {
            $('script').remove();
            $('link').remove();
            $('body').append('<script src="app.full.min.js"></script>');
            $('head').append('<link rel="stylesheet" href="app.full.min.css">');
        }))
        .pipe(gulp.dest('dist/'));
});</code>

顺便分享一下我们team的use-gulp项目 [https://github.com/Platform-CUF/use-gulp](https://github.com/Platform-CUF/use-gulp)

*   [2015年10月26日更新](https://segmentfault.com/q/1010000003908091/a-1020000003910843)
*   <a class="comments" data-id="1020000003910843" data-target="#comment-1020000003910843">2 评论</a>
*   <a>编辑</a>

 [![](https://sfault-avatar.b0.upaiyun.com/203/235/2032357569-5606c5159e075_big64)](https://segmentfault.com/u/hjzheng)

 [hjzheng](https://segmentfault.com/u/hjzheng "hjzheng")2.5k 声望

 答案对人有帮助，有参考价值0答案没帮助，是错误的答案，答非所问

gulp-useref

> [https://www.npmjs.com/package/gulp-useref](https://www.npmjs.com/package/gulp-useref)

*   [2015年10月26日回答](https://segmentfault.com/q/1010000003908091/a-1020000003908633)
*   <a class="comments" data-id="1020000003908633" data-target="#comment-1020000003908633">1 评论</a>
*   <a class="translate" data-canclick="1" data-type="answer" data-target="zh">翻译</a>
*   <a>编辑</a>

 [![](https://sfault-avatar.b0.upaiyun.com/733/999/733999308-58ff5b8ebbcb7_big64)](https://segmentfault.com/u/guox)

 [Mr_Betty](https://segmentfault.com/u/guox "Mr_Betty")956 声望

 答案对人有帮助，有参考价值0答案没帮助，是错误的答案，答非所问

gulp-usemin插件，你可能还需要gulp-rev
可以看看这个地址：[https://www.npmjs.com/package/gulp-usemin](https://www.npmjs.com/package/gulp-usemin)

*   [2015年10月26日回答](https://segmentfault.com/q/1010000003908091/a-1020000003908693)
*   <a class="comments" data-id="1020000003908693" data-target="#comment-1020000003908693">1 评论</a>
*   <a>编辑</a>

 [![](https://static.segmentfault.com/v-5964378c/global/img/user-64.png)](https://segmentfault.com/u/sunxh)

 [wyysf123](https://segmentfault.com/u/sunxh "wyysf123")61 声望

 答案对人有帮助，有参考价值0答案没帮助，是错误的答案，答非所问

这是我建的一个gulp-template
用了gulp-usemin、gulp-rev，
可以合并css和js并自动更换路径和添加版本号
[https://github.com/hxbo/gulp-project-template](https://github.com/hxbo/gulp-project-template)