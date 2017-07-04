# JS中的事件
## 事件的两部分
>1.事件的行为：浏览器天生赋予的行为（天生自带的属性，比如人出生就有吃饭这个行为）
>2.事件的绑定：给这个事件行为绑定一个方法（人在真正吃饭的时候执行的方法）
>**注意：**事件行为都是元素的私有属性，不管元素的行为有没有被触发都是存在的，假如没有绑定（就是触发的时候什么都没干）。
#### 异步执行的有
>定时器，回调函数，绑定的事件，ajax

#### DOM0级事件
>DOM0级事件的绑定：给一个元素的同一个行为只能绑定一次，如果多次绑定后面就会把前面的给覆盖了，原因就是给元素的属性赋了一个值（地址值）而已。
>DOM0级事件不存在兼容性，任何浏览器都可以用
#### DOM2级事件
>addeventlistener     是元素所属的EventTarget类原型上的共有属性,可以实现多次绑定（在IE 下不是按照顺序执行）
```
  box.addEventListener("事件的类型，就是事件行为不带on", function(){"给事件行为绑定的方法"},可选的参数false(默认冒泡阶段发生)/true（捕获阶段发生）)
```
>有兼容性。在IE下
```
box.attachEvent（“事件的类型”，function(){},false/true）
```
>绑定DOM2级事件的时候，为了移除的时候方便，第二个参数用函数名来写。

#### 事件移除
>DOM0级事件
```
onclick=null
```
>DOM2级事件
```
removeEventlistener("事件类型"，绑定的那个函数名，false/true)
```

#### 常用的事件行为（事件属性）
### 鼠标事件
>onabort  图像加载被中断触发的行为
>onload    当图片或者一个网页加载完成后触发的行为
```
<script>
  window.onload=function(){
       //当页面生的所有静态资源（HTML结构+CSS样式）全部加载完成才会触发的事件
}
</script>
```
>onerror    加载文档或者图片时发生错误就会触发这个行为
>onblur     元素失去焦点
>onfocus   元素获取焦点
>onchange  域的内容改变 (用作下面的三个标签)
```
<input  text="text/file">
textarea
select
```
>onclick   当元素被单击的时候
>ondbclick  当元素被双击的时候
>onreset   当重置按钮被点击的时候 （他是加在form上的）
>onsubmit  当提交按钮被点击的时候 （他是加在form上的）
>onunload   当用户退出页面之后触发的行为（他它是加在window下的）
>onresize    当浏览器窗口n发生改变（他是加在window上的 ）
>onmouseup  鼠标按键松开
>onmousedown  鼠标按键按下
>onmousemove  鼠标按住拖动
>onmouseover/onmouseenter  鼠标放上（用第一个放上事件的时候必须用下面第一个移开。第二个同理）//onmouseenter  不会冒泡
>onmouseout/onmouselevae   鼠标移开//onmouselevae不会冒泡
>onmousewheel   鼠标的滚轮


### 键盘事件
>onkeydown  键盘键按下
>onkeyup    键盘键松开
>onkeypress   键盘键按下在松开
>**注意：**当一个输入框按下键盘触发onkeydown 松开先触发onkeypress ，然后在触发onkeyup 。
>**注意：**没有输入内容（enter，tab，中文的时候输入法会阻止以下）就不会触发 



### 事件对象
>事件对象：当我们触发这个事件行为的时候，后面给他绑定的这个事件行为就会执行，而执行的时候，浏览器就会默认给他传一个参数，这个参数就是我们说的事件对象。（一般我们都是使用形参e来接受）
>**注意：1.**在IE 下浏览器不会默认给绑定的方法传参数，它的事件对象放在window . event。
>**注意：2.**在IE678中事件源是 srcElement
>**注意：3.**在低版本中没有pageX和pageY 
```	
box.onclick=function (e) {
    console.log(arguments[0]);
}
返回：MouseEvent {isTrusted: true, screenX: 23, screenY: 108, clientX: 23, clientY: 18…}
```
#### 鼠标事件对象
>MouseEvent  事件对象：记录当时触发这个事件那以瞬间的鼠标信息。里面有很多的私有属性
```
>e.clientX： 点击的那一下，鼠标距离浏览器左边的距离
>e.clientY： 点击的那一下，鼠标距离浏览器上边的距离
>e.pageX：点击的那一下，鼠标距离整个网页左边的距离
>e.pageY：点击的那一下，鼠标距离整个网页上边的距离
>e.target：事件源  谁执行的那个事件，事件源就是谁
```
>**注意：**两个事件同时触发，事件对象是一样的就是同一个事件对象。因为我们的鼠标就一个，你触发一次就记录一次信息。

### 键盘事件对象
>keyboardEvent
>keyCode：当前按下那个键的键值
```
空格：32
左：37
上：38
右：39
下：40
enter/return：13
shift:16
alt:18
control(ctrl):17
delete/backspace:8
del:46
```

### 事件委托
>给元素的事件行为绑定方法的时候，不是直接给当前元素绑定事件，而是给他的上级（一般都是父级或者最高级）绑定方法，通过判断事件源数谁来进行不同的操作，这就叫做事件委托（利用的就是事件传播机制，或者说是事件冒泡）


### 阻止事件默认行为
>a标签的默认行为：页面跳转，锚点连接
```
<a href="#"></a>;//点击不跳转
<a href="#box"></a>//box就是某一个元素的ID，当你点击a标签的时候，页面会展示到ID是box的那个元素上
当点击上面的a标签的时候，页面会跳转到ID是box的元素位置。		
<a href="javascript:;"></a>//阻止
<a href="javascript:void(0);"></a>//阻止

var a=document.getElementsByTagName("a");
a.onclick=function () {
		return false;
      };
a.onclick=function (e) {
e.preventDefault();//阻止默认行为，存在兼容性
//在IE低版本下
e.returnValue=false;
//兼容写法
//第一种：
e.preventDefault?e.preventDefault():e.returnValue=false;
//第二种：
e.preventDefault=e.preventDefault||function () {						e.returnValue=false;
 };
e.preventDefault();
            }
```
#### 为什么要阻止a标签的默认行为？
>1.为了SEO优化（搜索引擎优化），我们会给a标签的href一个真实的地址，但是单击的时候不会跳转。
>2.我们利用a标签的hover伪类，不存在兼容性。

### 事件传播机制（三部分）
>捕获阶段-->目标阶段-->冒泡阶段
>**注意：**先捕获在冒泡
>**注意：**我们只能阻止冒泡，不能阻止捕获

##### 捕获：
从外到里：body-->outer-->inter-->center(目标)
##### 冒泡
从里到外：center(目标)-->inter-->outer-->body

>在DOM0级事件发生在冒泡阶段
>**注意：**不管你给事件行为有没有绑定方法，依然会冒泡
>在DOM2级事件中，第三个参数就是用来控制在哪个阶段发生的。不传参数默认的是冒泡。
>false：表示的冒泡 true：表示的捕获

##### 阻止冒泡
>阻止冒泡：事件对象中的一个方法属性：e.stopPropagation（）；
>在IE 低版本，没有stopPropagation（）。有e.cancelBubble()  兼容写法
```
    e.stopPropagation?e.stopPropagation():e.cancelBubble();

```

### 滚轮事件
>onmousewheel
```
 var body=document.getElementById("body");
    body.onmousewheel=function (e) {
        console.log(e.wheelDelta);
    }
e.wheelDelta向上120
e.wheelDelta向下-120
```
>**注意：**在火狐中没有onmousewheel这个事件行为。用DOMMouseScroll。但是必须用DOM2级事件绑定
```
body.addEventListener("DOMMouseScroll",function (e) {
        console.log(e.detail);
        
    })
e.detail 向上-3
e.detail 向下3
```

### 鼠标和键盘的捆绑关系
>在IE中相当于给元素和鼠标捆绑在一起，就是鼠标移动，元素也移动
```
    box.setCapture()

```
>移除捆绑效果
```
box.releaseCapture()
```