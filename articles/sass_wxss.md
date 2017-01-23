# 通过sass实现对wxss动态生成

## 问题
* 微信小程序只支持wxss后缀的样式文件
* 小程序编辑器不好用写样式嵌套麻烦
* wxss组件/样式管理不方便

## 方案
1. 通过`gulp`动态编译`sass`文件并重命名的方式实现对`wxss`的支持。
2. 通过`linux/window`重命名命令，实现对sass编译后文件`css`重命名

## 实现
**gulp动态编译实现**

安装插件: 
* `gulp`
* `gulp-sass`
* `gulp-rename`
* `gulp-changed`

```javascript
var gulp = require("gulp");
var sass = require("gulp-sass");
var rename = require("gulp-rename");
var changed = require("gulp-changed");

//定义 sass文件源地址 wxss文件地址
var origin = "sass/**/*.scss";
var target = "./public/static/wxss";

//编译sass任务 =》 gulp sass
gulp.task("sass", function(){
    gulp.src(origin)
     //筛选个已经更改并且后缀是scss的文件
    .pipe(changed(target, {extension: "scss"}))
    //展开编译的文件
    .pipe(sass({outputStyle: "expanded"}))
    //后缀名改为wxss
    .pipe(rename(function(path){
        path.extname = ".wxss";
    }))
    .pipe(gulp.dest(target))
})


//默认任务 => gulp
gulp.task("default", function(){
    gulp.run("sass");
})

//监听sass文件变化，执行编译sass任务 => gulp watch:sass
gulp.task("watch:sass",function(){
    gulp.watch(origin, ["sass"]);
})
```

**重命名方式**
* `window`下通过：`ren *.css *.wxss`命令
* `linux`下通过：`rename .css .wxss *.css`(`rename 原字符串 新字符串 文件名`)

## 其他
在`windows`下安装`gulp-sass`可能会出现各种编译问题，具体可参考文章: [SASS安装过程中的一些问题解决](./sass_install.md)
