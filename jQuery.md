`$()  (jQuery())jQuery`函数，获取括号中指定的内容 

`html() `函数改变所匹配的 `HTML` 元素的内容`（innerHTML）`。

`$(selector).html(content)`

####attr()函数用于设置或返回当前jQuery对象所匹配的元素节点的属性值。
1. attr(传入属性名)：获取属性的值
2. attr(属性名, 属性值)：设置属性的值
3. attr(属性名,函数值)：设置属性的函数值
`attr(attributes)`：给指定元素设置多个属性值，即：{属性名一: “属性值一” , 属性名二: “属性值二” , … … }

####`.html`与`.text`的异同:
1. `.html`与`.text`的方法操作是一样，只是在具体针对处理对象不同
2.` .html`处理的是元素内容，`.text`处理的是文本内容
3.` .html`只能使用在HTML文档中，`.text` 在XML 和 HTML 文档中都能使用
4. `.val()`只能使用在表单元素上


####添加/删除样式类名
`.addClass()`
`.removeClass()`

###通过.css方法设置的样式属性优先级要高于.addClass方法

`.addClass`与`.css`方法各有利弊，一般是静态的结构，都确定了布局的规则，可以用`addClass`的方法，增加统一的类规则
如果是动态的HTML结构，在不确定规则，或者经常变化的情况下，一般多考虑`.css()`方式
* *
---

####on括号里面的click后面加上"button"就可以指定触发事件的元素了

`$body.on('click','button',function(){}`

|Event 函数|绑定函数至|
|:---||:---|
|`$(document).ready(function)`|将函数绑定到文档的就绪事件（当文档完成加载时）|
|`$(selector).click(function)`|触发或将函数绑定到被选元素的点击事件|
|`$(selector).dblclick(function)`|触发或将函数绑定到被选元素的双击事件|
|`$(selector).focus(function)`|触发或将函数绑定到被选元素的获得焦点事件|
|`$(selector).mouseover(function)`|触发或将函数绑定到被选元素的鼠标悬停事件|
|`$(selector).bind(event,data,function) `|规定向被选元素添加的一个或多个事件处理程序，以及当事件发生时运行的函数。|  
  
* *
---
			
####如果您希望在一个涉及动画的函数之后来执行语句，请使用 callback 函数。
```
$(selector).hide(speed,callback)

$("p").hide(1000,function(){

})
```

三个简单实用的用于 DOM 操作的 jQuery 方法：
	• `.text()` - 设置或返回所选元素的文本内容
	•`.html()` - 设置或返回所选元素的内容（包括 HTML 标记）
	• `.val()` - 设置或返回表单字段的值





####jquery过滤器
`.Filter()`过滤器   在结果集中过滤
```
<div id="grandpa">A
        <div id="pa">
            <div id="child1" class="child not-gay"></div>
            <div id="child2" class="child"></div>
            <div id="child3" class="child"></div>
        </div>
    </div>


$('#grandpa').find('.child').css('border','2px solid #999');
$('#child1').parent().css('border','2px solid #777');
$('#child1').parents('#grandpa').css('border','2px solid #444');
//child结果集  
$('.child').filter('.not-gay').css('background', 'red');

```
![](https://i.imgur.com/Fwcqz1l.png)

####属性操作
`.attr`(属性名称，属性值)（显性属性）
`.prop`(属性名称，属性值)（隐性属性）

####max和maxlength
`.max`用于验证数字
`.maxlength`用于验证字符串长度
