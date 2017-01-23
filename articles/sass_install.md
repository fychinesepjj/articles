# `sass`安装过程中的一些问题解决
## 说明
本文主要讨论`window`下安装`sass`时出现的问题解决。

## 关于Sass
`sass`安装分为两种：

1. `Sass`命令行
2. `Sass`插件

**Sass命令行**

首先下载`ruby`，然后通过`gem install sass`命令进行安装，后可直接运行`sass`命令。

**Sass插件**

通过与其他工具配合使用（webpack，gulp等），通常在安装过程中需要编译源码，常用的插件有：

1. `sass-loader`
2. `gulp-sass`

`sass`的安装问题多出现在插件的编译安装过程中，编译时有对`python`，`vcbuild`等组件的依赖，组件的缺失会导致一些莫名其妙的问题出现。

## 解决方法
1. 安装python2.7
2. 安装[.net framework 4.5.1+](https://www.microsoft.com/en-us/download/details.aspx?id=40773)
3. 安装Microsoft Visual C++ Build Tools：
   * [下载地址1](http://landinghub.visualstudio.com/visual-cpp-build-tools)，如安装过程中包下载失败请使用下载地址2
   * [下载地址2](http://www.microsoft.com/en-us/download/details.aspx?id=48159)
4. 执行`npm config set python python2.7`，`npm config set msvs_version 2015 --global`命令
5. 最后才安装`sass`插件

## 参考
[vcbuild problem](https://www.bountysource.com/issues/28025957-solved-using-visual-c-build-tools-2015-standalone-c-tools)