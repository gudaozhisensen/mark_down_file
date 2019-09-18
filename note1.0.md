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
    
# 全栈

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

##### 中间件:

  ##### 1.插件，对框架功能的补充

  ##### 2.流水线
 
     `.use()`引入中间件
     `.use(express.static())`//返回静态文件
     `res.sengFile(绝对路径文件名);`
 
    <!-- ----------------- -->
     res.send(any);
     res.sengFile(绝对路径文件名);     //跟static不一样，更灵活
     res.sendStatus(code);           //相当于原来的writeHeader + write + end
     res.redirect('location');      //相当于原来的setHeader + writeHeader

##### res.sendStatus() 状态码  
    server.get('/a',(req,res,next)=>{
      //.sendStatus();会根据状态码来进行相应的解析
      res.sendStatus(404);
      
      //相当于
      /*res.writeHeader(404);
      res.write('Not found');
      res.end();*/
      
      //一行代码解决原生node的三行
    });
##### res.redirect()
    res.redirect('location ');//重定向
<!-- -------------------------------------------------------------------------------- -->
     <!-- -------------------------------------------------------------------------------- -->
     
#### 数据交互: GET、POST
     
     
<!-- -------------------------------------------------------------------------------- -->
    server.get('/a',(req,res)=>{

    });

GET => `req.query` 直接用就行

#### 普通 POST=>  `body-parser`
    
通过`body.parser`解决POST数据解析问题
,body 解析的中间件

    const.body = require('body-parser');
    server.use(body.urlencoded({extend: false}));
    req.body;
#### 文件 POST=>  multer

`server.use(multer({dest:'文件路径'}).any());`
//`any()` 接收所有类型的文件

`req.body`

`req.files`//文件信息

    <!-- -------------------------------------------------------------------------------- -->
//client
    <form action="https://localhost.8080/upload" entype="multipart/form-data">
        <input type="file" name="f1">
        <input type="submit" value="提交">
      </form>

//server
    
    const multer require('multer');
    const express require('express');
    let server = new express;
    server.listen(8080);
    server.use(multer({dest:'upload/'}).any());

    server.post('/upload',(req,res)=>{
      consle.log(req.body);
      consle.log(req.files);
    })

<!-- -------------------------------------------------------------------------------- -->
     <!-- -------------------------------------------------------------------------------- -->

#### 用原生解决POST数据问题(自己写中间件)
    const querystring = require('querystring');
    server.use((req, res, next)=>{
      let arr = [];
      req.on('data',(data)=>{
        arr.push(data);
      });

      req.on('end',()=>{
      req.body = querystring.parse(Buffer.concat(arr).toString());

      next();
      });
    });

 <!-- -------------------------------------------------------------------------------- --> 
    innerHTML()效率比dom操作高,innerHTML()解析创建由浏览器完成
        
 <!-- -------------------------------------------------------------------------------- -->     
    <!-- -------------------------------------------------------------------------------- -->  
<!-- -------------------------------------------------------------------------------- -->  

<!-- p30 -->

### cookie
    cookie--存在浏览器里
    --4k
    --不安全
          
    session--存在服务器

    npm i cookie-parser cookie-session -D


#### cookie parser

    npm i cookie-parser -D

 发送/接收`cookies` 

`document.cookie`             前端获取`cookies`

`req.cookies`                   接收

`req.signedCookies`             带签名的`cookies`

`res.cookie(name,val, options)` 发送
    
    server.use(cookieParser('ghrkjiiu%0-340gfkjj^&$#3-9kjfkdj(*$)_FJIJIHGIHUI+#0-erfkdjgkfd'));//括号里为加密的密钥

    console.log(req.cookies);//普通cookies
    console.log(req.signedCookies);//加密的cookies

    res.cookie('b',5,{signed:true});
    res.send('aaa');

  <!-- -------------------------------------------------------------------------------- --> 

<!-- p30 -->

  #### cookie session

      npm i cookie-session -D

      server.use(cookieSession({
        keys:['hfjdh44oijigi5jkkjpoeruieewri','qoerieojqtejklvnjij','erotrjopqerueefjsleo'],
        secret:'xxx'
      }));

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
    
  ##### express服务器创建

    const express = require('express');
    let server = express();
    server.listen(8080);

    server.get('/xxx', () => {});

    server.post('/xxx', () => { });

    server.use('/xxx', () => {});  //通用，不限制方法
  
  
    
    server.get('/a',(req,res,next)=>{ 
      next();
    });
`res.write()`方法中只能传string和`buffer`

`res.send()` 兼容所有输出格式
   

    <!-- -------------------------------------------------------------------------------- -->
#####  res.sengFile()
    //把相对路径转换为绝对路径

    const pathlib = require('path');
      server.get('/a',(req, res, next)=>{ 
        res.patlib.resolve((a.txt));//针对字符串去做绝对路径解析，不管路径存不存在
    });
<!-- -------------------------------------------------------------------------------- -->

    <!-- -------------------------------------------------------------------------------- -->
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
    <!-- -------------------------------------------------------------------------------- -->
    <!-- 2019.05.08-->
    //闭包是函数和声明该函数的词法环境的组合。
    //闭包就是：一个内部函数可以记住它被创建时的环境。
    //闭包就是能够读取其他函数内部变量的函数，让这些变量的值始终保持在内存中。
    //A函数中定义了B函数并且它返回了B函数，那么不管B函数在哪里被调用或如何被调用，它都会保留A函数的作用域
    
    (function(){document.title=location.href;})();
    //第一对圆括号中的函数用作声明一个匿名函数，而最后的一对圆括号则用来执行这个函数。
    
    //立即执行函数

![](https://pic3.zhimg.com/d043f5554b4db3baf464606c15ab4c06_r.jpg)!
  
#   webpack  打包工具
  
    #webpack-cli   命令行工具
      npm i -g webpack //装的是  命令行工具
      
      #webpack       // 库
      npm i webpack//装的是库
       
     1.webpack本身
    //打包

    2.DevServer
    //开发服务器

    //--------------------------------------------------------------------------------

   

####     1. webpack.config.js  先新建的配置文件
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

#### 2.再建src文件，放js源文件，編譯前的文件
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

#### 3.打包命令 
      webpack webpack,config.js(webpack --config 要是改了默認文件名就要用這個命令)
      打包結束後就會出現dest文件夾

#### 4.dev-server虛擬开发服務器

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


#### 5. Loader--翻译

 //------------------------------------------------------------------------------------

    npm i babel-loader babel-core babel-preset-env -D

   *  `babel-loader`    给`webpack`用
   *  `babel-core`      `babel`核心
   *  `babel-preset-env` 环境预设


//------------------------------------------------------------------------------------


//-------------------05.14------------------------------------------------------------

90% 的`loader`

    module:{
      rules:[
        {test:正则,use:loader }
      ]
    }

//-------------------------------------------


//-------------------05.15------------------

  typeScript
   
   补充`js`没有的特性--类型，接口，抽象

  `ts-loader `

  `npm i -g `typescript`

//-------------------------------------------------------------------------------------


//-------------------05.18------------------------------------------------------------



运行 `tsc file.ts` => `file.js`

1. 类型
  变量、参数、返回值
  指明类型
    1.显式声明  let a:string;
    2.隐式声明  let a=12;

1. 联合声明
  `let a:(number|string)='12';`//可声明number或string
  `let a:(number|string)[]=[1,2,3,'avff '];`
2. 元组类型
  `let a:[number,boolean]=[12,true];`
3. 枚举类型

//-------------------------------------------------------------------------------------

2.类
  新的写法

3.高级特性
  抽象、接口


  

//-------------------------------------------------------------------------------------


//-------------------05.15------------------------------------------------------------

  # typeScript
   
补充js没有的特性--类型，接口，抽象

  `ts-loader `

  `npm i -g typescript`
 

  1. 类型
 变量、参数、返回值

      指明类型：

      1. 显式声明    let a:string;

      2. 隐式声明    let a =12;

  2. 类

 新的写法

     //访问修饰符--public/private/protected

`public` 任何人都可以修改
`private` 只有类内能修改
`protected` 只有类和子类能修改

//ts 能在变量、函数后指定

    let oDiv:number

    let oDiv:string

    let oDiv:boolean

    let oDiv:

    function():void{
   }

    //访问修饰符怎么用


“最小访问原则” `private->protected->public`

属性都是`private`和`protected`，方法可以是`public`

修饰符
`static` --- 静态成员  无需实例化即可调用

`const`  --- 只读成员  只读的，不能修改 

    class Person{
      public static user:string='blue';//静态成员
        constructor(name:string, private age:number){
          this.name=name;
      }
    }
    
    let p:Person = new Person('blue',18);
    console.log(Person.user);
    
    //tsc -t es5 xxx.ts 可选择用什么版本的es来编译 
    

  //存取器
    set/get    编译不了es3/4


 3.高级特性
     抽象、接口   
    //抽象类，只提供模板，不自己去实现，给子类提供规范

    //抽象、接口为了规范所有子类
    
    //抽象类只能作为父级使用，不能直接被实例化，抽象类必须被继承，父级不能使用这些方法。
    abstruct class Shape{
      
    }
    
    //Abstract 关键字同样可以用来声明抽象方法，抽象方法只包含一个方法名，而没有方法体。
    abstruct area():number; 
    
    
    //继承父类的子类要强制实现父类的抽象方法
    
    //interface  接口只能实现，不能继承，接口能继承接口 
    
    
    //1.对象有属性__proto__,指向该对象的构造函数的原型对象。
    //2.方法除了有属性__proto__,还有属性prototype，prototype指向该方法的原型对象。

  ![](https://pic1.zhimg.com/80/e83bca5f1d1e6bf359d1f75727968c11_hd.jpg)! 





  //-------------------------------------------


  //-------------------05.26------------------


    tsc --init 创建tsconfig.json 配置文件
    

泛型

    class Array<t>{

    }

    Array<int> arr = new Array<int>();



# vue 

vue 下的`template` 里 有且只有一个`div`
而且不能把html和body作为根

    MVC模式

1. `M Model`      模型   数据
2. `V View`       视图   表现层
3. `C Controller` 控制器 业务逻辑

    数据、逻辑、表现层分离，简洁，方便测试

    //--------------------------------------------------------------------------------

    MVP模式

    P->中间层

    //--------------------------------------------------------------------------------

    `MVVM`
    只把业务逻辑相关的代码放入，把表现相关的代码放视图层
    
    //--------------------------------------------------------------------------------

    `vue2.x`  模块化  


  1. 创建vm对象

    let vm = new Vue({
      el:根,
      data:{},
    });

 2. 视图层`(html)`写相应代码

    //-------------------------------------------------------------------------------- 

    1. 输出{{}}

#### 改变

    1. 不要直接操作DOM
    2. 数据为中心--数据驱动

        let vm = new Vue({
          el:'#div',//选择器,接管的部分,根元素
          data:{
            name: 
          }
        });
//-------------------------------------------------------------------------------- 

2. 数据绑定

    单向 {{输出}} 数据=>视图

    双向 `v-model`  数据<=>视图

//-------------------------------------------------------------------------------- 
    

3. 属性绑定

    `v-bind:`(:)

    `v-bind :`属性="数据"

    `:`属性="数据"

  //接受数组作为参数

  `:style="styleJson"`

  `:class="arr"`

//-------------------------------------------------------------------------------- 

4. 事件
    `v-on:`(@)

 //-------------------------------------------------------------------------------- 

5. 循环 `v-for`

`key` 数据自动同步到视图

`Vue`需要能把数据和DOM组件对应起来--提高性能

虚拟dom，在大型项目中比较合适
    :key-数据的ID
    :key="json.ID"
     
    v-for="val,key in 数组" 
    v-for="val,key in json"

 
 //--------------------------------------------------------------------------------

6. `v-show`  display

//-------------------------------------------------------------------------------- 

7. `v-if` 直接删除 

    特别是表单，就算是隐藏了，表单也是会提交的
  
//-------------------------------------------------------------------------------- 

8. 事件修饰符 
    `@事件.xxx`

//-------------------------------------------------------------------------------- 

  9. 计算后数据/属性 `(computed)`

  并不存在的数据，其实是个公式

  有缓存
  
 #### 应用：

  1. 频繁使用的复杂公式
  2. 需要监控的--一个固定的全局管理

    computed:{
      result: function(){
      return this.n1*this.n2;
      }
    }

      
完整版：
      
    computed:{
      result:{
        set: function(){},
        get: function(){} 
      }
    }

  `data`和`computed` 有相同的数据 `data`上的数据会覆盖`computed` 本身 

//-------------------------------------------------------------------------------- 

 10. 监听`(watch)`

    watch:{
      a(newVal,oldVal){
        console.log("a变了,从${oldVal}变成${newVal}");
      }
    }

//-------------------------------------------------------------------------------- 

建议所有的异步操作都在函数里，提升代码的可读性，基本上的异步操作都是数据交互

//-------------------------------------------------------------------------------- 

  11. 路由

`vue-router` 
路由切换的是组件,页面不变，变的是组件

  --SPA(单页应用)

  配置路由表->创建Vue对象,添加`router`(路由)->在根元素中添加`<router-view>`和`<router-link to=''>`

   // 带查询参数，下面的结果为 `/register?plan=private`
  `<router-link :to="{ path: 'register', query: { plan: 'private' }}">Register</router-link>`

    //1. 配置路由表
    let router= new Vuerouter({
      
        routers:[
          //路由定向,定向到不同的page
          {path:'/user'/, component:user}
          ,
          {path:'/company/:id',
           component:{
            template:'<div>卖家{{$router.params.id }}</div>', 
            }
          }
        ]
    });

  *  具体可以看 `sell-app`的`main.js`,每个组件单独放之后如何引入组件(分离后的组件要用`<template>`来包住)
  *   路由参数 `:id`,`vue`自带

      `#/xxx/:x/:x/:x?a=xx&b=xx`
      
      `$route.params` 获取`/:x/:x/:x`

      `$route.query` 获取`?a=xx&b=xx` 

    //2. 创建vue对象
    const vm = new Vue({
      el:'#app',
      router, //名字和值一样可以简写
      watch:{
        $route(newVal,oldVal){

        }  
      }
    })

    <body>
      <div id="app">
        <router-view></router-view> //router里注册的组件会在这里显示
        <router-link to='/user'>买家</router-link>
        <router-link to='/company'>卖家</router-link>

        hash
      </div>
    </body>
//-------------------------------------------------------------------------------- 

#### 关于路由
1. 由`hash`完成
2. `router-link`就是个`a`
3. `router-view`是个占位符，要显示的东西就会显示到这里
4. 一个组件`(component)`也是一个完整的vm


`data` 写到`component`内部必须是个`function`, return `json`

    component:{
      data(){
        return{
          count:12;
        };
      }
    }
    method:{
      fun(){
        alert("aaa");
      }
    }

`$route` 存放当前路由状态

//-------------------------------------------------------------------------------- 

#### 跳转之前确认
放在component里
beforeRouterUpdate(to,from,next){
    if(confirm('离开本页')){
      next();
    }
}


//-------------------------------------------------------------------------------- 
1. 路由
2. 参数

      `#/xxx/:x/:x/:x?a=xx&b=xx`

      `$route.params` 获取`/:x/:x/:x`

      `$route.query` 获取`?a=xx&b=xx`
3. 事件
    `beforeRouterUpdate(to,from,next)`

//-------------------------------------------------------------------------------- 
#### 11.1 嵌套路由

    let router = new VueRouter(){
      routes:[
        {
          path:'/user',
          component:{template:'<div>用户<router-view></router-view></div>'},
              //子路由
          children:[
            //1
            {
              path:'info',
              component:{template:'<span>用户信息</span>'},
              children:[
                ...
              ]
            },
            //2
            {
              path:'avatar',
              component:{template:'<span>头像</span>'}
            }
          ]
        },
        {
          path:'/company',
          component:{template:'<div>公司<router-view></router-view></div>'},
          //子路由
          children:[
            //1
            {
              path:'update',
              component:{template:'<div>更新<router-view></router-view></div>'},
              children:[
                ...
              ]
            },
            //2
            {
              path:'show',
              component:{template:'<div>展示<router-view></router-view></div>'}
            }
          ]
        }
      ]
    }

    <div id="app">
        <router-link to="/user/info">用户信息</router-link>
        <router-link to="/user/avatar">头像</router-link>
        <router-link to="/company/update">更新</router-link>
        <router-link to="/company/show">展示</router-link>
        <router-view></router-view>
    </div>
//-------------------------------------------------------------------------------- 
#### 11.2 命名路由(用路由的名字进行索引)
  1. 全路径
    2. `json->{name:'名字',params:{},query:{}}`

     name: 'i', 
     <router-link :to="{name:'i', params:{id:3}}">用户信息</router-link>

    {
          path:'/user',
          component:{template:'<div>用户<router-view></router-view></div>'},
              //子路由
          children:[
            //1
            {
              path: 'info',
              name: 'i', 
              component:{template:'<span>用户信息</span>'},
              children:[
                ...
              ]
            },
            //2
            {
              path:'avatar',
              name:'a',
              component:{template:'<span>头像</span>'}
            }
          ]
        }

    <div id="app">
        <router-link :to="{name:'i',params:{id:3}}">用户信息</router-link>
        <router-link to="/user/avatar">头像</router-link>
        <router-link to="/company/update">更新</router-link>
        <router-link to="/company/show">展示</router-link>
        <router-view></router-view>
    </div>
//-------------------------------------------------------------------------------- 
#### Router 构建选项
linkActiveClass:'active' //**链接激活时使用的css类名**


`$route`  信息
`$router` 操作   

//-------------------------------------------------------------------------------- 



#### 注册组件

##### 全局注册

    Vue.components('my-component',{
      template:'<App>'
    })

    var app = new Vue({
      el:'#app'
    })

##### 局部注册

    var app =new Vue({
      el:'#app',
      components:{
        'my-components':App
      }
    })
    
*区别好像就是放不放在new Vue里*

<!--  -->
在`table`中使用组件,用`is`属性挂载,`is="my-component"`

//--------------------------------------------------------------------------------

    import ListItem from 'list_item';

    export default{
     compenents:{
       ListItem
     }
    }//声明之后可以<ListItem></ListItem>使用

//-------------------------------------------------------------------------------- 
  
  父组件给子组件传递数据

  
  `this.$attrs`  父级传过来的所有数据
  this.txt = this.attrs['str'];

#### 组件间通信

    <father-component></father-component>//父组件,和子组件的挂载点father-component
    vue.component('father-component',{
      props   : ['message'],             //传递父组件数据,props声明
      template: '<h3>{{message}}</h3>'  //子组件和子组件接收父组件数据
    })
  *props可以将数据从父组件传入子组件，*

  *slot可以将html从父组件传入子组件。*

父-> 子  :xxx="数据"(父级)    子级 $attrs.xxx (子级)

子 -> 父 函数 

父组件的模板中包含子组件
 
  372c7a45a932043a820931d948f3ddaa72d1206d

  372c7a45a932043a820931d948f3ddaa72d1206d 



//--------------------------------------------------------------------------------
  ### Axios
  ajax库

//-------------------------------------------------------------------------------- 

    server.use(async (cts,next)=>{
       ctx.set('Access-control-Allow-Origin','*');
    });




    Vue.component('todo-list',{
      template:''
    })

* 把axios放在main.js里

      import axios from 'axios';
      Vue.prototype.ajax = axios;
    
* 模块内部
      
      (await this.ajax('url')).data;

//--------------------------------------------------------------------------------

#### axios
ajax库

    axios({
      method:'get(default)/post',
      url:'/user/1.txt',
      dataType:'json',
    }).then(res->{
        console.log(res);
    },res->{
        console.log('失败');
    });

//-------------------------------------------------------------------------------- 

#### fecth 
原生js改进版的ajax

      this.item = await (await fecth('url')).json();

      //fecth出来的是promise对象，data在json对象里，json也 是个promise对象，await两次之后才能拿到数据


//-----------------------------------20190614--------------------------------------------- 


### vue 状态统一管理

### vuex
1. state -- 状态(全局唯一)

2. getter   获取状态

3. mutation  修改状态操作

4. action    提交mutation,动作

 ![](https://vuex.vuejs.org/vuex.png)! 

#### *(1)创建*

    const store = Vuex.store({
      //里面有json参数
      strict true,
      state:{
        count:0
      },
      mutations:{
        addCount(state,arg){
          state.count++;
          //addCount:state => state.count++
        }
      },
      actions:{
         _//用actions去调mutations_
        addCount(store(是个json,大多数要里面的commit),arg){

          或//addCount({commit},arg){
          //  commit('addCount',arg);
          }
        }
      },
      getters:{}
    }); 

#### *(2)注册*

_通过在根实例中注册 `store` 选项，该 `store` 实例会注入到根组件下的所有子组件中，且子组件能通过 `this.$store` 访问到。_

    vue.use(Vuex);
    //store 引入
    const app = new Vue({
      store:store
      
    });

#### *(3)组件里-用(可跨组件)*


_由于 store 中的状态是响应式的，在组件中调用 store 中的状态简单到仅需要在计算属性中返回即可。触发变化也仅仅是在组件的 methods 中提交 mutation。_
    
    computed:{
      count(){
        return this.$store.state.count;
      }
    },
    methodd:{
      fnAdd(){
        this.$store.dispacth('addcount',arg);
      }
    }


#### 分发 `Action`
_Action 通过 `store.dispatch` 方法触发_

`this.$store.dispatch('action名字',参数);`

  组件-> `dispacth` -> `action commit` ->`mutation`(操作`state`对象,修改的具体方法) `state.xx` -> `state`

//-------------------------------------------------------------------------------- 


组件 `dispatch->  action commit -> mutution state.xxx -> state`

<!--  -->
    import Vuex from 'vuex'

    Vue.use(Vuex);
    Vue.config.productionTip = true;
    const store = Vuex.store({
      strict true,//严格模式--只能由mutation修改状态
      state:{
        count:0;
      },
      munation:{
        addCount(state,arg){
          state.count++;
        }, 
        minuCount(state,arg){
          state.count--;
        }
      }
    });
 

//-------------------------------------------------------------------------------- 
在 `Vuex` 中，`mutation` 都是同步事务
手动触发`action`，异步操作都放`action`        适合异步
`getters`，同步操作都放`getters`             适合同步

结论：
数据交互--`getter`
其他异步操作--`action`

computed：数据变化时自动计算值
getters 不适合数据交互以外的操作

1.数据搭好---vuex+axios/fetch
2.组件---展示、逻辑

//-------------------------------------------------------------------------------- 

`srcset` 属性
用于浏览器根据宽、高和像素密度来加载相应的图片

    <picture>

      //屏幕尺寸小于767px加载xxx.jpg
      <source media="(max-width:767px)" srcset="xxx.jpg">
      </source>

      <source media="(min-width:768px)" srcset="yyy.jpg">
      </source>
      
    </picture>




//-------------------------------------------------------------------------------- 

#### vue v-model 修饰符

`v-model.lazy` 失焦或按回车后才更新   

`v-model.number` 将输入转为Number类型
 
`v-model.trim` 过滤首尾空格

`<card>`

`data`必须是函数，以函数的形式`return`出去                                                                                  

//-------------------------------------------------------------------------------- 
                                                               

ref=""  vue DOM 操作

    <div class="menu-wrapper" ref="menuWrapper">

    this.$refs.menuWrapper//操作


//-------------------------------------------------------------------------------- 

#### 父组件调用子组件方法
子组件上定义`ref="refName"`, 父组件的方法中用 `this.$refs.refName.method` 去调用子组件方法

    <template>
      <child ref="myChild"></child>
    </template>
//-------------------------------------------------------------------------------- 

#### slot(插槽)

 *props可以将数据从父组件传入子组件，*  传入数据的名字名字必须得一样，有'-'的，子组件用驼峰     

  *slot可以将html从父组件传入子组件。*



`food-list-hook` 表明只是用来被`js`选择的`class`,并没有实际的样式效果


vue 方法命名规则
仅限于被组件内部调用的方法，一般在方法前加下划线 `_initCalc`
可以被外部调用,一般就正常写                    `calculator`


    @media only screen and(max-width:320px){

    }//唯一關鍵字阻止不支持與媒體功能媒體查詢從應用指定的樣式舊的瀏覽器。


https://www.thymeleaf.org/doc/tutorials/3.0/usingthymeleaf.html
https://ultraq.github.io/thymeleaf-layout-dialect/

https://waylau.gitbooks.io/thymeleaf-tutorial/docs/introduction.html

https://github.com/cloudfavorites/favorites-web


//-------------------------------------------------------------------------------- 

<!-- p34  爬虫 -->

<!-- 2019-08-05 -->





<!-- 2019-08-06 -->

`JSON.parse()`//把一個JSON字串轉換成 JavaScript的數值或是物件

`JSON.stringify()`//将一个JavaScript值(对象或者数组)转换为一个 JSON字符串



`npm config list` 查看config 列表
`npm config set http(https)-proxy http://your_proxy_ip:port`  
`proxy_ip`为`netstat`所得的ip
可以解决proxy 问题