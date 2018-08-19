#ES6
---
####常量
`//ES5中常量的表示`
>     Object.defineProperty(window,"PI2",{
>     value:3.1415926,
>     writable:false,
>     })


`//ES6`
>     const PI=3.1415926;
>     //const声明变量，就必须立马初始化，不能以后在赋值 

###作用域
####变量提升

1. 即变量可以在声明之前使用，值为`undefined`。
2. 代码块内外有同名变量，变量提升会是内层变量覆盖外层变量。

>     //变量提升是对变量表达式的引用，不是对变量值的引用
>     var s="Hello";
>     for(var i=0;i<s.length;i++){
>     console.log(s[i]);
>     }
>     console.log(i);//5
>     //i只用来控制循环，循环结束后，没有消失，泄露成了全局变量


`console.table`以表格形式输出