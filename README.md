# javascript-css-common
##常用代码总结  

javascript和css的常用代码总结。在平时工作和学习中，我们会遇到经常使用的片段，如果每次都去网上搜索的话，会浪费很多的时间，因此在这里把常用的代码总结一下！

##目录
  1. [CSS初始化样式reset.css](#reset)
  2. [去除浮动clearfix](#clearfix)
  3. [js操作cookie](#js-cookie)
  4. [css强制换行/自动换行/强制不换行](#word-wrap)
  5. [table边界的样式](#table-border)
  6. [div上下左右居中](#div-center)
  7. [图片上下左右居中](#img-center)
  8. [js字符串翻转](#js-str-reverse)
  9. [iPad页面适配框架](#ipad_adap)
  10. [google html5.js](#google_html5_js)
  
####<a id="reset" name="reset">1. CSS初始化样式reset.css</a>  
不同的浏览器对各个标签默认的样式是不一样的，而且有时候我们也不想使用浏览器给出的默认样式，我们就可以用reset.css去掉其默认样式

```css
body, h1, h2, h3, h4, h5, h6, hr, p, blockquote, dl, dt, dd, ul, ol, li, pre, form, fieldset, legend, button, input, textarea, th, td { margin:0; padding:0; }
body, button, input, select, textarea { font:12px/1.5tahoma, arial, \5b8b\4f53; }
h1, h2, h3, h4, h5, h6{ font-size:100%; }
address, cite, dfn, em, var { font-style:normal; }
code, kbd, pre, samp { font-family:couriernew, courier, monospace; }
small{ font-size:12px; }
ul, ol { list-style:none; }
a { text-decoration:none; }
a:hover { text-decoration:underline; }
sup { vertical-align:text-top; }
sub{ vertical-align:text-bottom; }
legend { color:#000; }
fieldset, img { border:0; }
button, input, select, textarea { font-size:100%; }
table { border-collapse:collapse; border-spacing:0; } 
```

####<a id="clearfix" name="clearfix">2. 去除浮动clearfix</a>  
通常我们在有浮动元素的情况下，会在同级目录下再创建一个`<div style="clear:both;"></div>`；不过这样会增加很多无用的代码。此时我们用`:after`这个伪元素来解决浮动的问题，如果当前层级有浮动元素，那么在其父级添加上clearfix类即可。  
```css
.clearfix:after {
  content: "\00A0";
  display: block;
  visibility: hidden;
  width: 0;
  height: 0;
  clear: both;
  font-size: 0;
  line-height: 0;
  overflow: hidden;
}
.clearfix{zoom:1}
```

####<a id="js-cookie" name="js-cookie">3. js操作cookie</a>

```javascript
var  cookie = {
     //写cookies
     setCookie: function (name, value){
         var  Days = 365;
         var  exp =  new  Date();
         exp.setTime(exp.getTime() + Days*24*60*60*1000);
         document.cookie = name +  "=" + escape (value) +  ";expires="  + exp.toGMTString();
     },
     
     //读取cookies
     getCookie: function (name){
         var  arr,reg= new  RegExp( "(^| )" +name+ "=([^;]*)(;|$)" );
         if (arr=document.cookie.match(reg)) 
             return  unescape(arr[2]);
         else 
             return  null ;
     },
     
     //删除cookies
     delCookie: function (name)
     {
         var  exp =  new  Date();
         exp.setTime(exp.getTime() - 1);
         var  cval= cookie.getCookie(name);
         if (cval!= null ) document.cookie= name +  "=" +cval+ ";expires=" +exp.toGMTString();
     }
}
```

####<a id="word-wrap" name="word-wrap">4. css强制换行/自动换行/强制不换行</a>
```css
/* 强制不换行 */
div{
  white-space:nowrap;
}

/* 自动换行 */
div{ 
  word-wrap: break-word; 
  word-break: normal; 
}

/* 强制英文单词断行 */
div{
  word-break:break-all;
}
```

####<a id="table-border" name="table-border">5. table边界的样式</a>
```css
table { border :  1px  solid  #B1CDE3 ; padding : 0 ; border-collapse :  collapse ; table-layout : fixed ;  margin-top : 10px ;}  
table td { height : 30px ; border :  1px  solid  #B1CDE3 ;  background :  #fff ;   font-size : 15px ;  font-family :Microsoft YaHei;  padding :  3px  3px  3px  8px ; color :  #4f6b72 ;  width : 160px ;}
```

####<a id="div-center" name="div-center">6. div上下左右居中</a>  
```css
div{
  position:absolute;
  width:400px;
  height:300px;
  left:50%;
  top:50%;
  margin-left:-200px;
  margin-top:-150px;
}
```

####<a id="img-center" name="img-center">7. 图片上下左右居中</a>  
一种常用的方式是把外层的div设置为table-cell；然后让内部的元素上下左右居中。当然也还有一种方式，就是把img当做div，参考6中的代码进行设置。  
CSS代码如下：  
```css
.content{
  width: 400px;
  height: 400px;
  border: 1px solid #ccc;
  text-align: center;
  display:table-cell;
  vertical-align:middle;
}
```
html代码如下：  
```html  
<div class="content">
  <img src="./4.jpg" alt="img">
</div>
```

####<a id="js-str-reverse" name="js-str-reverse">8. js字符串翻转</a>  
js中没有直接对字符串进行反转的，需要我们先转换成数组，然后使用数组中的`reverse()`方法翻转，最后在把数组拼接回字符串。  
```javascript
var str = "abcdefg";
var revs = str.split("").reverse().join("");
console.log(revs);
```

####<a id="ipad_adap" name="ipad_adap">9. iPad页面适配框架</a>  
这是一个适配iPad页面的大致框架，包括竖屏和横屏
```css
iPad 适配
/* ipad 竖屏 */
@media only screen 
and (min-device-width : 768px) 
and (max-device-width : 1024px) 
and (orientation : portrait) { 
    body{ color:#000; }
    /* … */
}

/* ipad 横屏 */
@media only screen 
and (min-device-width : 768px) 
and (max-device-width : 1024px) 
and (orientation : landscape) {
    body{ color:#000; }
    /* … */
}
```

####<a id="google_html5_js" name="google_html5_js">10. google html5.js</a>
这是Google提供的js框架，使IE8及以下的浏览器支持html5新标签
[html5.js 链接](http://html5shim.googlecode.com/svn/trunk/html5.js)
```javascript
/*
 HTML5 Shiv v3.7.0 | @afarkas @jdalton @jon_neal @rem | MIT/GPL2 Licensed
*/
(function(l,f){function m(){var a=e.elements;return"string"==typeof a?a.split(" "):a}function i(a){var b=n[a[o]];b||(b={},h++,a[o]=h,n[h]=b);return b}function p(a,b,c){b||(b=f);if(g)return b.createElement(a);c||(c=i(b));b=c.cache[a]?c.cache[a].cloneNode():r.test(a)?(c.cache[a]=c.createElem(a)).cloneNode():c.createElem(a);return b.canHaveChildren&&!s.test(a)?c.frag.appendChild(b):b}function t(a,b){if(!b.cache)b.cache={},b.createElem=a.createElement,b.createFrag=a.createDocumentFragment,b.frag=b.createFrag();
a.createElement=function(c){return!e.shivMethods?b.createElem(c):p(c,a,b)};a.createDocumentFragment=Function("h,f","return function(){var n=f.cloneNode(),c=n.createElement;h.shivMethods&&("+m().join().replace(/[\w\-]+/g,function(a){b.createElem(a);b.frag.createElement(a);return'c("'+a+'")'})+");return n}")(e,b.frag)}function q(a){a||(a=f);var b=i(a);if(e.shivCSS&&!j&&!b.hasCSS){var c,d=a;c=d.createElement("p");d=d.getElementsByTagName("head")[0]||d.documentElement;c.innerHTML="x<style>article,aside,dialog,figcaption,figure,footer,header,hgroup,main,nav,section{display:block}mark{background:#FF0;color:#000}template{display:none}</style>";
c=d.insertBefore(c.lastChild,d.firstChild);b.hasCSS=!!c}g||t(a,b);return a}var k=l.html5||{},s=/^<|^(?:button|map|select|textarea|object|iframe|option|optgroup)$/i,r=/^(?:a|b|code|div|fieldset|h1|h2|h3|h4|h5|h6|i|label|li|ol|p|q|span|strong|style|table|tbody|td|th|tr|ul)$/i,j,o="_html5shiv",h=0,n={},g;(function(){try{var a=f.createElement("a");a.innerHTML="<xyz></xyz>";j="hidden"in a;var b;if(!(b=1==a.childNodes.length)){f.createElement("a");var c=f.createDocumentFragment();b="undefined"==typeof c.cloneNode||
"undefined"==typeof c.createDocumentFragment||"undefined"==typeof c.createElement}g=b}catch(d){g=j=!0}})();var e={elements:k.elements||"abbr article aside audio bdi canvas data datalist details dialog figcaption figure footer header hgroup main mark meter nav output progress section summary template time video",version:"3.7.0",shivCSS:!1!==k.shivCSS,supportsUnknownElements:g,shivMethods:!1!==k.shivMethods,type:"default",shivDocument:q,createElement:p,createDocumentFragment:function(a,b){a||(a=f);
if(g)return a.createDocumentFragment();for(var b=b||i(a),c=b.frag.cloneNode(),d=0,e=m(),h=e.length;d<h;d++)c.createElement(e[d]);return c}};l.html5=e;q(f)})(this,document);
```

