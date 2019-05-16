```
<script type="text/javascript">
const mysql = require('mysql');
//連接池

let db = mysql.createPool(host: "localhost", user: "root", password: "" , port: "3306", maxconection:10);
db.query();

--------------
// 服务端接收
const http = require('http');
const io = require('socket.io');
const fs = require('fs');
let httpServer = http.createServer();
httpServer.listen(8080);
let wsServer = io.listen(httpServer);
let aSock=[];
wsServer.on('connection',sock=>{
aSock.push(sock);
sock.on('msg',str=>{ 
aSock.forEach(s=>{
if (s!=sock) {
sock.emit('msg',str);//发送给非自己的客户端数据
}
})
})
});
sock.on('disconnect',()=>{
var n = aSock.indexOf(sock);
if (n>-1) {
aSock.splice(n,1);//当客户端断开连接时从第n位删除一个元素
}
})
//客户端发送和接收
const http = require('http');
const io = require('socket.io');
const fs = require('fs');
sock.emit('msg',oTxt.value);//把填入的数据发给服务端
sock.on('msg',str=>{
...
})//接收服务端发送过来的数据
//客户端判断连接状态
sock.on('connect',()=>{
console.log('已连接');
})
sock.on('disconnect',()=>{
console.log('连接断开');
})

---------------------------------------------------------------------------
跨域 
不存在跨域，跨域是浏览器的限制

---------------------------------------------------------------------------
//
let data = new FormData();
Array.from(ev.dataTransfer.files).forEach(file=>{
	data.append('f1',file);
});

//原生Ajax 
let oAjax = new XMLHttpRequest();
oAjax.open('GET',url,true);
oAjax.send();
oAjax.onreadystatechange=function(){
if (oAjax.readyState==4) {
if (oAjax.status>=200 && oAjax.status<300 || oAjax.status=304) {
alert("seccess");
}else{
alert("fail");
}
}
}
---------------------------------------------------------------------------
multiple
<input type="file" id="fi" multiple/>

---------------------------------------------------------------------------

拖拽事件
ondragenter 拖着东西进入    addEventListener('dragenter',()=>{},false);
ondragleave 拖着东西离开   addEventListener('dragleave',()=>{},false);
ondragover  悬浮   addEventListener('dragover',()=>{},false);
ondrop      松手上傳   addEventListener('drop',()=>{},false);

oBox.ondragenter =function(){
oBox.innerHTML="松手上传";
return false;//阻止默认事件
}//鼠标进入oBox范围是就会变化

oBox.ondragover = function(){
      console.log("aaa");
      return false;//阻止默认事件,不阻止那么ontrop永远不会发生
    }//


oBox.ondrop =function(ev){

console.log(ev.dataTransfer.files);
return false;//阻止默认事件
}

(addEventListener)綁定之後的阻止默認事件

//ev事件对象，是事件里传递数据的对象

--------------------------------------------------------------------------- 
//文件上传进度监控
oAjax.upload.onprogress = function(ev){//function 放在前面 放在AJAX创建的位置 open 和 send之间
 ev.loaded   //完成
 ev.total //总共

 ev.loaded/ev.total   =>0-1
}  
//AJAX 2.0才有进度监控
oAjax.upload.addEventListener('progress',function(ev){
console.log(ev);
},false);


1.upload必须放在send前面
2.以前上传--POST
加了upload--option、POST

--------------------------------------------------------------------------- 
數據庫結構：  數據字典
接口格式：    接口文檔


--------------------------------------------------------------------------- 
oAjax.onprogress 下載進度
oAjax.upload.onprogress 上傳進度
--------------------------------------------------------------------------- 
HTML5--DOM3
官方：所有DOM3(HTML5)事件都得綁定
--------------------------------------------------------------------------- 
斷點上傳--普通html做不到，客戶端ok
移動端web不行
移動端app可以
通過content-range頭實現
--------------------------------------------------------------------------- 
如果兩次上傳同一個文件，第二次還會上傳嗎
瀏覽器：每次都得重新上傳
客戶端檢測文件內容


--------------------------------------------------------------------------- 
//2019.01.09

//畫圖：
canvas   位圖---放大失真
svg      矢量圖--無限縮放
VML      矢量圖

---------------------------------------------------------------------------
//2019.01.10
箭头函数内外this保持不变
ex：
//1
document.onclick = function(){
let arr = {1,2,3};
//箭头函数外 document
arr.a = ()=>{
//箭头函数内 document
alert(this);
};
arr.a();
}


//2
//箭头函数外 window
document.onclick = ()=>{
//箭头函数内window
let arr = {1,2,3};
//箭头函数外 window
arr.a = ()=>{
    //箭头函数外 window
        alert(this);
    };
    arr.a();
}

//四个地方都保持不变

</script>

<!-- css -->
<!-- linear radial 渐变其实是图片渐变
用trasform 的时候加上个初始值 -->

<style type="text/css" media="screen">

transform: rotate(0deg);
transform: rotate(90deg);




 /*-------------------------------------------------------------------------------- */

/*盒模型：物体占据空间的大小*/

css3样式不改变盒模型 不会改变物体真实的大小
移动端特别爱用transform 

 /*--------------------------------------------------------------------------------*/
/*2019.01.22*/
 transition: 1s all ease;
 /*1s 為時間 all 為樣式 ease 為運動形式*/

 transition: 1s width, 1s height, 1s color, ease-out;

transition 數字類的都能進行變換 width length color font-size



animation

/*1.定義*/
/*2.調用*/

@keyframes name{
    0%{width: 200px; height: 200px; font-size:14px; background: #ccc;}/*初始狀態 0-25% width 改變*/
    25%{width: 400px; height: 200px; font-size:14px; background: #ccc;}/*到25-50%的時候 height開始改變*/
    50%{width: 400px; height: 400px; font-size:14px; background: #ccc;}/*到50-75%的時候 font-size開始改變*/
    75%{width: 400px; height: 400px; font-size:30px; background: #ccc;}/*到50-75%的時候 bgcolor開始改變*/
    100%{width: 400px; height: 400px; font-size:30px; background: red;}
}


.box:hover {
   animation-name:name;/*所使用的動畫名*/
  animation-duration:5s;/*動畫持續時間*/
  animation-timing-function:ease;
}

 /*--------------------------------------------------------------------------------*/
/*2019.01.22*/



 /*移動端開發*/
1.移動端佈局
2.touch
3.庫
4.響應式


/*1.viewport*/


盒模型
flex
rem

/* 有的手機不認initial-scale=1.0  就要用到 maximum-scale=1.0, minimum-scale=1.0來代替 */


/*--------------------------------------------------------------------------------*/


 /*2.盒模型 */
普通盒子 width=width + padding + margin padding、margin往外加 

box-sizing:border-box;
/*能實現浮動*/
border-box 以邊框為準，要加的padding、border往裡擠
,margin 還是往外加

/*--------------------------------------------------------------------------------*/


/*3.flex-彈性盒模型*/

.box{display:-webkit-box;}

    display: -webkit-box; /* Chrome 4+, Safari 3.1, iOS Safari 3.2+ */
    display: -moz-box; /* Firefox 17- */
    display: -webkit-flex; /* Chrome 21+, Safari 6.1+, iOS Safari 7+, Opera 15/16 */
    display: -moz-flex; /* Firefox 18+ */
    display: -ms-flexbox; /* IE 10 */
    display: flex; /* Chrome 29+, Firefox 22+, IE 11+, Opera 12.1/17/18, Android 4.4+ */

    display：box； 是老规范，要兼顾古董机子就加上它。
    flexbox flex 是新规范，老机子不支持的。

    display:flex;  
    1,具備border-box的能力
    2，對padding,margin,border都能自適應
    3，跟max-width, min-width 配合

/*--------------------------------------------------------------------------------*/


    /*4.rem*/
    px：絕對尺寸
    em：相對尺寸 自身字體
    rem：相對尺寸 root字體 html字體

    在不同的屏幕尺寸下，只需要調整HTML元素font-size，方便，性能高
    一切尺寸都用rem

    基準寬度：480px
    基準字大小: 10px
    width:480px -> 48rem
    height:55px -> 5.5rem


</style>

<!-- -------------------------------------------------------------------------------- -->
<script type="text/javascript">

    console.log(oDiv.classList);//輸出div的list

 </script>


 <!-- -------------------------------------------------------------------------------- -->

<!-- 2019.01.24 -->

HTML5
classList  輸出class 的序列
classList.remove 移除class
classList.add      加上class

相當於jquery 的addclass() 和 removeclass()


<!-- 移動端的佈局 -->
viewport
flex
rem
絕對不要用px


<script type="text/javascript">
	
	document.documentElement.style.fontSize = document.documentElement.clientWidth/48 + 'px';
</script>


<!-- -------------------------------------------------------------------------------- -->

2019.01.25

變量命名:　下劃線分割單詞
函數命名：從第二個單詞開始把每個單詞的第一個字母大寫

對象  對象裡的數據可以通過屬性和方法訪問 屬性：隸屬於某個特定方法的變量，方法：是只有某個特定形象才能調用的函數


getAttribute()  查詢屬性的名稱  不能通過document對象調用
setAttribute(attribute,value) 屬性節點值進行设置/(存在)修改
.attr()

<!-- -------------------------------------------------------------------------------- -->

<!-- 2019.02.13 -->

text-indent:; 首行縮進

<!-- -------------------------------------------------------------------------------- -->

<!-- 2019.02.15 -->

mouse事件 mousedown move up

dom3事件都应绑定
touch事件 touchstart move end 

mouse touch融合  pointer事件

gesture 手势 (多點)

<!-- -------------------------------------------------------------------------------- -->

<!-- 2019.02.18-->

匿名函数不能被删除



<!-- getComputedStyle -->

getComputedStyle

element.style 读取的只是元素的内联样式，即写在元素的 style 属性上的样式；
而 getComputedStyle 读取的样式是最终样式，包括了内联样式、嵌入样式和外部样式。

element.style 既支持读也支持写，我们通过 element.style 即可改写元素的样式。
而 getComputedStyle 仅支持读并不支持写入。我们可以通过使用 getComputedStyle 读取样式，通过 element.style 修改样式
我们可以通过使用 getComputedStyle 读取样式，通过 element.style 修改样式。


 
<!-- targetTouches -->
targetTouches 是一个只读的 TouchList 列表，含有当前接触屏幕的所有触摸点所对应的 Touch 对象。
就是触摸时的点

<!-- querySelector()  -->

querySelector() 方法返回匹配指定选择器的第一个元素。

querySelectorAll()返回所有符合的元素。


<!-- -------------------------------------------------------------------------------- -->

<!-- 2019.02.19-->

下拉刷新



跳了  跳到十九節
iscroll.js and hammer.js


<script type="text/javascript">

function loaded() {
  			myScroll = new IScroll( "#example", { 
  				// 父元素，可以拖動的是子元素
  			});
  		}

  	</script>

<!-- IScroll參數 -->

bounce：		是否允許拖過  true(預設)、false
scrollX：	允許水平拖拽 true、false(預設)
scrollY：	允許垂直拖拽 true(預設)、false
freeScroll：允許自由拖拽
momentum：  物理引擎

p元素有margin  


<!-- -------------------------------------------------------------------------------- -->

<!-- 2019.02.20-->

事件 probeType--探測優先級

1    低		定時探測
2    中		實時檢測用戶拖拽
3    高		實時檢測用戶拖拽+實時檢測運動本身		自動

iscroll事件：
scroll
 
beforeScrollStart   手指按下去
scrollStart 		第一次移動
scroll              滾動中
scrollEnd   		手指抬起來
scrollCancel        手指按下去，就抬起來


<!-- -------------------------------------------------------------------------------- -->

<!-- 2019.02.26-->
 .map会返回一个新的矩阵(数组)
 map set 可迭代

<!-- canvas -->

canvas 
不能保存图形  不能修改图形 也没有事件

<!-- 顺序 -->
beginPath()  清除之前的一切路径，重新开始(不覆盖之前的操作)，一切路径之前一定要beginPath()
moveto()
lineto()
stroke()		线性
strokeStyle()	颜色
lineWidth()		线宽

fill()			填充
closePath() 闭合当前路径   可加可不加

<!-- 矩形 -->
rect() 		 路径操作
strokeRect() 路径操作
fillRect()   路径操作
clearRect(x, y, width, height)   擦除指定区域内的所有内容

window.onresize()  自适应

<!-- -------------------------------------------------------------------------------- -->

<!-- 2019.02.27-->

requestAnimationFrame()通知瀏覽器我們想要產生動畫

clientX clientY 	获取鼠标距浏览器显示窗口的长度
offsetX offsetY     被点击元素距被触发dom左上角为参考原点的长度  chrome 包含边框  IE FF不包含边框
screenX screenY     触发点相对于显示器屏幕

<!-- -------------------------------------------------------------------------------- -->

<!-- 2019.02.28-->

圆
.arc(x,y,r,sAngle,eAngle,counterclockwise);(x坐标，y坐标，半径，弧起始點(弧度為單位)，弧終點(弧度為單位)，true(逆时针) or false(defalut 顺时针))
角度转弧度 n*(Math.PI/180)
弧度转角度 n*(180/Math.PI)

Math.sin() 參數以弧度為單位
Math.cos() 參數以弧度為單位

```
    <!-- -------------------------------------------------------------------------------- -->
    <!-- 2019.03.26-->    
    
    `join()` 方法會將陣列中所有的元素連接、合併成一個字串，並回傳此字串。

    let arr=[];
    arr.push(`2323`,`2323`);
    arr.join('-');
    //用的是"`",也不知道为什么
    <!-- -------------------------------------------------------------------------------- -->
    
    <!-- 2019.03.29-->
    富文本编辑器
    Tinymce
    
    <!-- -------------------------------------------------------------------------------- -->
    <!-- 2019.04.01-->
    //跳了Echarts2(25)、 D3(26) 27 和 28 
    
    //全栈
    node.js --原生框架(Express、 KOA)
    框架(angular、vue、react)
    app(混合式app)
    微信--公众号、小程序
    
    原生node.js
    数据交互
    数据库
    多进程
    
    express 
    依赖回调函数
    KOA
    generator/async
    
    koa@1  1.几版本 generator
    koa@2  2.几版本 generator+async
    koa@3  3.几版本 async
    
    
    <!-- -------------------------------------------------------------------------------- -->
    <!-- 2019.04.02-->
    
    `express.write()`方法中只能传string和`buffer`

    `.send()` 兼容所有输出格式

     中间件:
     1.插件，对框架功能的补充
     2.流水线
 
     `.use()`引入中间件
     `.use(express.static())`
     `res.sengFile(绝对路径文件名);`
 
    <!-- ----------------- -->
     res.send(any);
     res.sengFile(绝对路径文件名);     //跟static不一样，更灵活
     res.sendStatus(code);           //writeHeader + write + end
     res.redirect('location');
 
    server.get('/a',(req.res)=>{
      //.sendStatus();会根据状态码来进行相应的解析
      res.sendStatus(404);
      
      //相当于
      /*res.writeHeader(404);
      res.write('Not found');
      res.end();*/
      //一行代码解决原生node的三行
    });
    
    res.redirect('location ');//重定向
     <!-- -------------------------------------------------------------------------------- -->
     
     数据交互: GET、POST
     
     
     <!-- -------------------------------------------------------------------------------- -->

        innerHTML()效率比dom操作高,innerHTML()解析创建由浏览器完成
        
        
          
    <!-- -------------------------------------------------------------------------------- -->
    <!-- 2019.04.25-->
    
    //移除清理
    //可以用
    overflow:hidden/auto //,都有一个隐式的高度自适应
    
    <!-- -------------------------------------------------------------------------------- -->
    <!-- 2019.04.26-->
    //水平、垂直居中用flex方法实现
    display: flex;
    align-items: center;
    justify-content: center;
    
    <!-- -------------------------------------------------------------------------------- -->
    <!-- 2019.05.06-->
    //跳了29.3 30 31 32 33
    
    npm koa koa-static koa-better-body koa-router -D
    
    //express 和 koa引用的区别
    
    //const express = require('express');
      const koa = require('koa');
    
    //let server = express();
      let server = new koa();
      
      server.listen('8080');
    
    
    //koa强依赖router，所以每次都要把router引进
    const router = require('koa-router');
    let r1 = router();
    server.use(r1.routes());
    
    //以当前所在的目录为基准解析路径
    const path = require("path"); 
    path.resolve('www');
    // 返回: '/www'
    
      <!-- -------------------------------------------------------------------------------- -->
    <!-- 2019.05.08-->
    //闭包是函数和声明该函数的词法环境的组合。
    //闭包就是：一个内部函数可以记住它被创建时的环境。
    //闭包就是能够读取其他函数内部变量的函数，让这些变量的值始终保持在内存中。
    //A函数中定义了B函数并且它返回了B函数，那么不管B函数在哪里被调用或如何被调用，它都会保留A函数的作用域
    
    (function(){document.title=location.href;})();
    //第一对圆括号中的函数用作声明一个匿名函数，而最后的一对圆括号则用来执行这个函数。
    
    立即执行函数

![](https://pic3.zhimg.com/d043f5554b4db3baf464606c15ab4c06_r.jpg)!
  
###   webpack  打包工具
  
    #webpack-cli   命令行工具
      npm i -g webpack //装的是  命令行工具
      
      #webpack       // 库
      npm i webpack//装的是库
       
     1.webpack本身
    //打包

    2.DevServer
    //开发服务器

    //--------------------------------------------------------------------------------

   

#####     1. webpack.config.js  先新建的配置文件
     //webpack基本配置
    /*module.exports={
      entry:'文件名',
      output:{
      path:'结果目录',
      filename:'结果目录名'
      }
    };*/   
    
    //栗子
    const pathlib = require('path');

    module.exports={
      mode:'develpment'/'production',
	    entry:  './src/index.js', //入口文件
	    output:{
		  path:pathlib.resolve('dest/'),//目标文件
		  filename:'bundle.js'//打包後形成的文件
	}
    }

    //多入口
    /*entry:{
      名字:'入口文件地址',
      //index:'./src/index',
      //test:'./src/1',
    },
    output:{
      path:'xxx',
      filename:'[name].bundle.js'
      }*/

      //栗子
      const pathlib = require('path');

    module.exports={
      mode:'develpment'/'production',
    entry: {
        index: './src/index.js',
        test :'./src/1.js'
    }, //入口文件
    output:{
        path:pathlib.resolve('dest/'),//目标文件
        filename:'[name].bundle.js'
    }
    }

##### 2.再建src文件，放js源文件，編譯前的文件
      在模块里写函数没有全局一说
        //------------------------------------------
        
      一般文件輸出用的是`export default{}`
      沒有輸出`default`，就只要想要輸出的內容輸出就行
      `import` 自定義參數名 `from`  `./js文件名`   
      `node`不认`import`
      
       //------------------------------------------
    ES6模块化
    export default xxx;         //作为模块本身被输出     import xxx from '...';
    export let a=12,b=5;        //输出模块的东西         import {a,b} from '...';
  
    //------------------------------------------

##### 3.打包命令 
      webpack webpack,config.js(webpack --config 要是改了默認文件名就要用這個命令)
      打包結束後就會出現dest文件夾

##### 4.dev-server虛擬开发服務器

      1. 安装
      
      cnpm i webpack webpack-cli webpack-dev-server -D

     devsever:{
       contentBase: pathlib.resolve('static');
       port       :8090,
       hot        :true,//热更新
      }

      執行命令：webpack-dev-server


      2. 快速启动命令
        在`package.json`中配置命令:
        
        "scripts":{
          "start": "webpack-dev-server --inline --config 2-devserver.webpack.js"
        },
          --inline指的是整个页面的刷新
          执行命令：npm start


     3. 热更新，要加上`plugins`
        const Webpack= require('webpack');

        plugins[
          new Webpack.hotModuleReplacementPlugins()//模块热更新
        ],
        devsever:{
          hot        :true,//热更新
      }

      //静态文件热更新要在dev-server命令行里加上--watch

        historyApiFallback: true   //加了所有的访问都会定向到index.html,为了适应路由  404 will be fallback to index.html


##### 5.Loader--翻译

 //------------------------------------------

    npm i babel-loader babel-core babel-preset-env -D

   *  babel-loader    给`webpack`用
   *  babel-core      `babel`核心
   *  babel-preset-env 环境预设


//------------------------------------------


//-------------------05.14------------------

90% 的loader
module:{
  rules:[
    {test:正则,use:loader }
  ]
}

//-------------------------------------------


//-------------------05.15------------------

  typeScript
   
   补充js没有的特性--类型，接口，抽象

  ts-loader 

  npm i -g typescript
