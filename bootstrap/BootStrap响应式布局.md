---
title: BootStrap响应式布局
---

#### 一、响应式发开原理

一个网页页面，也许在PC屏幕上可以正常显示。但是在移动端小屏幕上，所有的组件可能就挤在了一起，很不协调。反过来在手机端很合适的布局，来到大屏幕上操作显示起来又很不方便。
为了解决各种屏幕的显示问题，我们需要用到响应式开发。响应式开发就是根据屏幕大小自动响应，自动调整的一种开发模式。
原理如下：

```css
@media screen and (max-width:800px){
    .container{
        width:100%;
    }
}
@media screen and (min-width:801px){
    .container{
        width:750px;
    }
}
```

使用`@media`获取屏幕的大小，根据屏幕的尺寸动态调整`css`样式，从而达到一次开发，多平台共用的目的。

#### 二、`BootStrap`布局

`BootStrap`是一种使用响应式开发的前端框架，开发者可以使用框架预定义的`container`类、栅格布局系统和各种样式。

##### 1.准备工作

在用`BootStrap`之前，需要引入`bootstrap`文件和`jQuery`文件。两者都可以下载到本地引入或者输入网址引入。除此以外还要在`html head`中添加三个`meta`元素和一个`if`条件注释。我认为在一开始的学习过程中，不需要过于关注这些前缀的意义，等拥有一定基础之后再返回头了解也可以。可以直接从`BootStrap`官网的复制下来。
引用自`v3.bootcss.com/getting-started/`:

```html
<!doctype html>
<html lang="zh-CN">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <!-- 上述3个meta标签*必须*放在最前面，任何其他内容都*必须*跟随其后！ -->
    <title>Bootstrap 101 Template</title>

    <!-- Bootstrap -->
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/3.4.1/css/bootstrap.min.css" integrity="sha384-HSMxcRTRxnN+Bdg0JdbxYKrThecOKuH5zCYotlSAcp1+c8xmyTe9GYg1l9a69psu" crossorigin="anonymous">

    <!-- HTML5 shim 和 Respond.js 是为了让 IE8 支持 HTML5 元素和媒体查询（media queries）功能 -->
    <!-- 警告：通过 file:// 协议（就是直接将 html 页面拖拽到浏览器中）访问页面时 Respond.js 不起作用 -->
    <!--[if lt IE 9]>
      <script src="https://cdn.jsdelivr.net/npm/html5shiv@3.7.3/dist/html5shiv.min.js"></script>
      <script src="https://cdn.jsdelivr.net/npm/respond.js@1.4.2/dest/respond.min.js"></script>
    <![endif]-->
  </head>
  <body>
    <h1>你好，世界！</h1>

    <!-- jQuery (Bootstrap 的所有 JavaScript 插件都依赖 jQuery，所以必须放在前边) -->
    <script src="https://cdn.jsdelivr.net/npm/jquery@1.12.4/dist/jquery.min.js" integrity="sha384-nvAa0+6Qg9clwYCGGPpDQLVpLNn0fRaROjHqs13t4Ggj3Ez50XnGQqc/r8MhnRDZ" crossorigin="anonymous"></script>
    <!-- 加载 Bootstrap 的所有 JavaScript 插件。你也可以根据需要只加载单个插件。 -->
    <script src="https://stackpath.bootstrapcdn.com/bootstrap/3.4.1/js/bootstrap.min.js" integrity="sha384-aJ21OjlMXNL5UyIl/XNwTMqvzeRMZH2w8c5cRVpzpU8Y5bApTppSuUkhZXN0VxHd" crossorigin="anonymous"></script>
  </body>
</html>
```

##### 2.布局容器

`BootStrap`框架提供给开发预定义好的`container`类和`container-fluid`类作为布局容器，这两个类会根据屏幕的尺寸自动调整大小，不需要开发者自己通过`@media`定义。`container`类不会占满整个屏幕，容器左右两端留有部分空白。而`container-fluid`类的容器会占满整个屏幕，所以`container-fluid`类只适合移动端开发。所以我认为开发过程中主要使用`container`。

```html
<div class="container">container容器</div>
<div class="container-fluid">container-fluid容器</div>
```

![bootstrap容器](/images/BootStrap响应式布局/容器.png "bootstrap容器")
container容器根据屏幕大小调整容器大小的对照表如下：

|          | 超小屏幕 手机（<768px) | 小屏幕 平板（>=768px） | 中等屏幕 桌面显示器（>=992px） | 大屏幕 大桌面显示器（>=1200px） |
| :------- | :--------------------: | :--------------------: | :----------------------------: | :-----------------------------: |
| 类前缀   |        .col-xs-        |        .col-sm-        |            .col-md-            |            .col-lg-             |
| 容器宽度 |          自动          |         750px          |             970px              |             1170px              |

##### 3.栅格系统

BootStrap提供了布局容器，接下来需要考虑的就是如何在容器内进行布局。BootStrap给我们提供了栅格系统这个概念。我们可以把container容器想象成为一张白纸，栅格系统把这张纸分成若干行，每行划分为12个大小相等的格子。开发者只需要规定每个盒子占多少个格子即可。我们通过具体事例还理解整个系统。

###### （1）行和列

首先创建container容器，然后在容器中创建行(row)，行左右两个均有15px的padding。

```html
<div class="container">
    <div class="row">第一行</div>
    <div class="row">第二行</div>
</div>
```

![行](/images/BootStrap响应式布局/行.png)
行是布局的基本单位，每行都被分为均等的12份，也就是12列(column)。我们先创建几个div，然后规定每个div占几份就可以完成布局。
上面第二小节提到的类前缀表示在对应屏幕大小时，盒子占的格子数量。
举例：
.col-xs-6:代表在超小型屏幕设备中该盒子占六个格子，两个盒子占满一行。
.col-sm-4:代表在小型屏幕设备中该盒子占四个格子，三个盒子占满一行。
.col-md-3:代表在中型屏幕设备中该盒子占三个格子，四个盒子占满一行。
.col-lg-2:代表在大型屏幕设备中该盒子占两个格子，六个盒子占满一行。

```html
<div class="container">
    <div class="row">
        <div class="col-xs-6 col-sm-4 col-md-3 col-lg-2">2</div>
        <div class="col-xs-6 col-sm-4 col-md-3 col-lg-2">1</div>
        <div class="col-xs-6 col-sm-4 col-md-3 col-lg-2">3</div>
        <div class="col-xs-6 col-sm-4 col-md-3 col-lg-2">4</div>
        <div class="col-xs-6 col-sm-4 col-md-3 col-lg-2">5</div>
        <div class="col-xs-6 col-sm-4 col-md-3 col-lg-2">6</div>
    </div>
</div>
```

![xs](/images/BootStrap响应式布局/xs.png)
![sm](/images/BootStrap响应式布局/sm.png)
![md](/images/BootStrap响应式布局/md.png)
![lg](/images/BootStrap响应式布局/lg.png)
如果一行中所有盒子所占的格子数量少于12个，盒子会靠左排列，右边会空出来。
如果一行中所有盒子所占的格子数量超过12个，多出来的盒子会另起一行。
![moreorless](/images/BootStrap响应式布局/moreorless.png)

###### （2）列嵌套、列偏移和列排序

列嵌套：在row中创建一个盒子（比如div），盒子中还可以创建新的row（div中加row），这个嵌套进去的新row在布局的时候也使用栅格系统。

```html
<div class="container">
    <div class="row">
        <div class="col-md-6">
            <div class="row">
                <div class="col-md-6">1</div>
                <div class="col-md-6">2</div>
            </div>
        </div>
        <div class="col-md-6">3</div>
    </div>
</div>
```

![列嵌套](/images/BootStrap响应式布局/列嵌套.png)
列偏移：通过向左侧增加margin值达到将标签向右移动的目的。使用.col-md-offset-*，在对应尺寸中向右移动对应的格数。

```html
<div class="container">
    <div class="row">
        <div class="col-md-8 col-md-offset-2">1</div>
        <div class="col-md-2">2</div>
    </div>
</div>
```

![列偏移](/images/BootStrap响应式布局/列偏移.png)
列排序：使用`.col-md-push-*`把标签向左移动对应格数，使用`.col-md-pull-*`把标签向右移动对应格数。

```html
<div class="container">
    <div class="row">
        <div class="col-md-8 col-md-push-4">1</div>
        <div class="col-md-2  col-md-pull-8">2</div>
    </div>
</div>
```

![列排序](/images/BootStrap响应式布局/列排序.png)

###### （3）隐藏

.hidden-xs、.hidden-sm、.hidden-md、.hidden-lg在对应尺寸的屏幕中隐藏该标签

