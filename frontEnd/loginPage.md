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
linear-gradient():生成一个渐变色图片;第一个参数表示旋转角度,第二个第三个参数分别表示渐变的两种颜色.
> [UI设计配色网站](https://flatuicolors.com/)
````CSS
body {
    min-height: 100vh;
    background-image: linear-gradient(120deg,#3498db,#9b59b6)
}
````
#### 2.3