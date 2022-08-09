---
Build a login page
---
# 从零开始编写一个登录页面
> [参考视频连接](https://www.bilibili.com/video/BV1x4411k7Vh)

### 1.创建form表单
先在body中创建一个form表单,form表单内分成五个部分:标题,用户名输入框,密码输入框,登录按钮和提示信息.
````html
<form action="index.html" class="login-form">
    <h1>Login</h1><!--标题-->
    <div class="textbox"><!--用户名输入框-->
        <input type="text"/>
        <span data-spaceholder="Username"></span>
    </div>
    <div class="textbox"><!--密码输入框-->
        <input type="text"/>
        <span data-placeholder="Password"></span>
    </div>
    <input type="submit" class="loginbtn" value="Login"/><!--登录按钮-->
    <div class="buttomtext"><!--底部提示信息-->
        Don't have account? <a href="#">Sign up</a>
    </div>
</form>
````
值得注意的是:
span标签中的data-placeholder属性属于placeholder是input输入框在未输入数据时默认显示的内容.
placeholder有两种添加方式:
- 1.直接在input标签中添加:`<input type="text" placeholder="Username"/>`
- 2.新建一个span标签，在span标签中添加placeholder属性，然后绝对定位覆盖到input上面

视频中使用的是第二种方式。
### 2.编写CSS样式
#### 2.1设置全局样式
margin和padding宽度都为0;
text-decoration是下划线这类字体装饰;
font-family和字体的选择有关
box-sizing与盒子的容量相关
> 1.[box-sizing](https://blog.csdn.net/cxd3341/article/details/100936159)
> 2.[CSS盒子模型](https://www.runoob.com/css/css-boxmodel.html)
````CSS
* {
    margin:0;
    padding:0;
    text-decoration: none;
    font-family: montserrat;
    box-sizing: border-box;
}
````
#### 2.2body标签样式
在body标签中设置高度并添加背景图片
min-height设置最小高度.
vh和vm是一组距离单位;vh是长度,vm是宽度。1vh表示视窗长度的1%,1vm表示视窗宽度的1%。
视窗的长度和宽度是根据使用设备动态变化的,PC端就是浏览器窗口大小,移动端就是移动设备界面大小.
此处必须要设置高度,因为body的子元素form表单使用的是absolute定位,如果不设置高度,body会出现高度坍塌,高度变成0;
linear-gradient():生成一个渐变色图片;第一个参数表示旋转角度,第二个第三个参数分别表示渐变的两种颜色.
> [UI设计配色网站](https://flatuicolors.com/)
````CSS
body {
    min-height: 100vh;
    background-image: linear-gradient(120deg,#3498db,#9b59b6)
}
````
#### 2.3form表单样式
设定表单的长、宽、边框、背景和定位
padding属性上下左右可以分着写，也可以简写。两个参数对应上下和左右，四个参数就分别是上下左右。
border-radius把边框变成圆角
> [position定位](https://www.runoob.com/css/css-positioning.html)

left和top辅助position进行定位,百分比参照的是父元素的长度.
transform:translate同样也是对元素进行定位,第一个元素是x轴,第二个元素是y轴,百分比参照的是自身的长度.
> [CSS中的百分比的应用](https://zhuanlan.zhihu.com/p/93084661)
````CSS
.login-form{
    height: 580px;
    width: 360px;
    padding: 80px 40px;
    border-radius: 10px;
    background: #f1f1f1;
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%,-50%);
}
````
> [什么时候用 margin？什么时候用 padding？](https://blog.csdn.net/jnshu_it/article/details/88941743)

#### 2.4标题
text-align设置文字居中;
因为form表单已经设置的padding内边距,所以h1标签只需要添加margin-bottom控制和下面元素的距离.
````CSS
.login-form h1{
    text-align: center;
    margin-bottom: 60px;
}
````

#### 2.5输入框
两个输入框的样式相同.
通过添加border-bottom的方式设置下滑线
````CSS
.textbox{
    border-bottom: 2px solid #adadad;
    position: relative;
    margin: 30px 0px;
}

.textbox input{
    font-size: 15px;
    color: #333;
    border: none;
    width: 100%;
    outline: none;
    background: none;
    padding: 0 5px;
    height: 40px;
}
````
输入框的动画:
span和input默认是在同一行,对span添加的CSS样式会显示到input后方.
需要把span标签设置为block元素,使span移动到input下方.
span::before和span::after是在span的前面和后面添加content内容.
> [CSS中的::after ::before](https://zhuanlan.zhihu.com/p/281419920)

加号`+`是相邻兄弟选择器,选择相邻的标签.
本项目中的`.focus + span::before`的意思就是选择focus类标签相邻的span标签,并在span前面添加内容.
到目前为止的html页面中没有class为focus的标签,为什么这里有.focus类选择器呢?
在js(需要引入jQuery)中把添加focus类这个动作与onfocus事件绑定就能达到生成动画的目的.
`transition: .5s`意思是动画持续0.5秒钟.
z-index设置堆叠元素显示优先级
[z-index](https://m.php.cn/article/464345.html)
````CSS
.textbox span{
    display:block;
}

.textbox span::before{
    content:attr(data-placeholder);
    position: absolute;
    top: 50%;
    left: 5px;
    color:#adadad;
    transform:translateY(-50%);
    z-index: -1;
    transition: .5s;
}

.textbox span::after{
    content: '';
    position: absolute;
    width: 0%;
    height: 2px;
    background-image: linear-gradient(120deg,#3498db,#8e44ad);
    transition: .5s;
}

.focus + span::before{
    top: -5px;
}

.focus + span::after{
    width: 100%;
}
````

````Html
<script type="text/javascript">
    // document.querySelector(".textbox input").onfocus=function(){
    //     this.classList.add("focus");
    // };
    // document.querySelector(".textbox input").onblur=function(){
    //     if(this.value==""){
    //         this.classList.remove("focus");
    //     }
    // }
    //querySelector只能选中一个元素,而不是符合条件的所有元素.不好用
    //querySelectorAll能选中所有符合条件的元素,但是返回的是一个数组,需要分别设置onfocus的值

    $(".textbox input").on("focus",function(){
        $(this).addClass("focus");
    })
    $(".textbox input").on("blur",function(){
        if($(this).val()==""){
            $(this).removeClass("focus");
        }
    })
</script>
````

#### 2.6登录按钮
background-size设置为200%,按钮中只能显示一半背景图片,hover事件让背景图片向右移动生成动画.
cursor悬停时光标样式变化.
````CSS
.loginbtn{
    display: block;
    width: 100%;
    height: 50px;
    border: none;
    background-image: linear-gradient(120deg,#3498db,#8e44ad,#3498db);
    background-size: 200%;
    color: #fff;
    outline: none;
    cursor: pointer;
    transition: .5s;
}

.loginbtn:hover{
    background-position: right;
}
````

#### 2.7提示信息
````CSS
.bottomtext{
    margin-top: 60px;
    text-align: center;
    font-size: 13px;
}
````