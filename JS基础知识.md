
# JS基础知识

## 了解JS
 > 1. .JS是运行在浏览器
  2. JS是唯一一门可以和用户直接交互的语言
  3. .JS是一门“轻量级”的解释型脚本语言
    -解释型：代码边解释边运行
    -轻量级：语言不严谨
  4.  JS安全性低，很容易被篡改   
  5.  JS是单线程语言（从上到下执行）

## JS的组成
>ECMAScript，ECMA是一个组织，这个组织规定了js的基本规范。ECMAScript实际上是JS 的API（JS的规范）
>DOM  Document Object Model 文档对象模型 是操作document（文档对象）  文档对象是文件的顶级对象
>BOM 浏览器对象模型（Browser Object Model）操作的是浏览器，浏览器的顶级对象是window(浏览器对象)
## JS的作用

>一般JS是用来获取和操作DOM元素，或者操作浏览器
-  数据交互
-  数据绑定
-  动态效果

## JS的引入方式
>js是不能独立运行的，需要依靠html文档运行在浏览器中，所以我们需要将JS引入到html中。
>-行内式（一般应用于简单的时间）
```
<a href="javascript:vido (0)"></a>
表示占位，不会跳转也不会刷新页面
```
>-内嵌式
>外联式

>JS代码一般写在整个html文档的最后面，因为要先加载document的所有内容，然后在将JS添加到每一个DOM对象上
>如果想要想在上面，那么必须写如下的代码
```
<script>
（让浏览器把所有的静态资源（结构和样式）加载完成在执行这里的代码）
window.onload=function(){
      JS代码写在这里
}
</script> 
```

>如果将JS代码写在外联式的元素中间，这部分的代码是无效的

## JS的输出方式

让用户察觉到页面的变化

>第一种:  alect（“”）  在页面弹出弹框
>第二种：confirm（“”）弹出弹框，有确定和取消
>第三种:  document .write 直接在页面上输出出内容
                              也可以识别代码      
```
<script type="text/javascript">
    document.write("你好");
    document.write("<p style='color:red';>我是p标签</p>");
</script>（在页面中是红色的 	）
```
>第四种:  console.log()  向控制台输出一条信息
>第五种:  console.dir()   向控制台输出一个对象的所有内置属性
 -内置属性:  天生自带的属性,内置属性可以改变属性值
 -自定义属性:  认为给这个对象添加的属性名和是属性值.
 >innerHTML  可以获取指定元素内容和向指定元素内容添加内容，可以识别标签，获取的时候所有的内容包括标签都会获取出来。
```
  var str="123";
    oLis.innerHTML+="<a href="https//www.baidu.com">'+str+'</a>
    (这样添加不会覆盖原来的内容)
```
 
 >innerText    可以获取指定元素内容和向指定元素内容添加内容，不可以识别标签，获取的时候 只获取文本。
 
 >innerHTML  ，innerText    在向元素内添加内容的时候，会将原来的内容替换掉
 
 >innerHTML   可以获取一个元素内的所有内容（包括元素的文本）
 >innerText      只能过去一个元素内的文本内容


>获取的语法：
   元素innerHTML   =  要添加的内容
   元素innerText     = 要添加的内容

>在JS中等号（=）是复制的意思，将等号右侧的值赋给等号左侧
>“.”的意思相当于“的”


## JS的命名规范

>-  严格区分大小写test,Test代表不同的对象
>-  不能以数字为开头 1txt 是错误的 txt1 是正确的。数字要放在最后面
>-  可以使用$  _  字母  数字组成的名称
>-  推荐使用驼峰命名法
```
  -  多个有意义的单词在一起的时候，第一个单词首字母小写，其余单词首字母大写  backgroundColor
```
>-  变量命名时，可以使用匈牙利命名法
```
  -  将数据类型的首字母，写在命名的前面
  -  对象object-- > oDiv
  -   数组array --> a
```
>-  命名的时候，不能使用关键字和保留字
```
     -关键字：ECMAScript中规定了一些单词具有特殊的含义，这些单词不能用作命名，例如 var let...
   -保留字：    ECMAScript中规定了一些单词未来可能将他们定义为关键字（关键字不够用了，可以用保留字替换）
```

## JS中的变量

>变量：一个可变的量
变量相当预一个容器，这个容器想放什么都可以
变量的作用：用来储存值或者代表值


>怎么定义一个变量：
      关键字 变量名；--> var name;
      变量只定义不赋值的时候，获得变量返回undefined

>给变量赋值：
   关键字 变量名=值；--> var name=123;


## JS中的数据类型
### 基本数据类型
   >-数字   number
    >-字符串 string
    >-布尔  boolean
    >-null
    >-undefined
 
#### 判断具体分类：    

### 1.数字number 
```
哪些值是number?
整数 0 小数 NaN(not a number)

判断一个值是否为数字：isNaN
从第一个有效数字开始到最后一个有效数字结束，中间不能不能有数字意外的任何东西，包括空格等。否则是“NaN”
返回值
符合条件为ture -->不是一个数字
不符合条件为flase-->是一个数字

方法：
方法一：number（value）将其他数据类型转为数字数据类型
返回值：数字或者NaN
方法二：parseFloat()浮点数（小数）
返回值：数字或者NaN
方法三：parseInt()整数
返回值：数字或者NaN
parseFloat()和parseInt()的方法，都是从之指定值中去分离一部分数字，一般指定的值要么是数字要么是字符串。如果传入的值不是数字也不是字符串，先将值转化为字符串，然后在字符串中数字。
工作机制：parseFloat 识别小数点
         parseInt   只识别整数
         
在JS中，除了变量名之外的所有内容基本上都是字符串，字符串在JS中需要用引号包起来
```

##### 数字与其他数据类型判断：

```
对象-->number
-将对象转为字符串 调用toString（）方法
-再将字符串转为数字 调用number（）方法
对象{}-->"[object object]"-->NaN
数组[]-->""-->0
（数组转化就是把[]换成“”，里面不论是什么数字，都会放在“”里。

字符串 （string）-->numner
-字符串转为数字 调用number（）方法

布尔 boolean-->number
-调用number（）方法
ture 为 1
false 为 0

null-->number 
-调用number（）方法
null 为 0

undefined-->number
-调用number（）方法
undefined 为NaN
```    

### 2.布尔 boolean

>返回值只有两个：true（真）或false（假）


>那些值为假，那些值为真？
 -0   NaN   ""   null   undefined为假，其余都为真

##### 怎样判断一个值是真还是假？
>Boolean(value)将其他数据类型转为布尔类型的方法不需要转换其他数据类型，直接根据五个值是假，其余是真的，判断是真还是假。

>逻辑运算：
！value 先将value转为布尔，然后取反
！0 -->！Bollean(0) -->!false-->ture
!!取反在取反（实际就值相当与直接转化为布尔）

### 3.字符串 string

>字符串：在js中字符串是一个变量，用来储存文本的，用引号包裹，字符串在js中不具有任何的意义，也没有任何的功能

```
{}-->"[object object]"(不论{}里面有没有东西都会转化为"[object Object]")
[]-->""
0-->"0"
null-->"null"
undefined-->"undefined"
```
>拼接字符串
 就是将两个或多个字符串用“+”链接起来。如果用变量来代表字符串的时候，变量不能用引号包起来

其他数据类型如果遇到字符串拼接的时候，会默认先转为字符串数据类型，然后在拼接
例如：[]+‘abc’-->""+"abc"-->"abc"
 
```
<script type="text/javascript">
     var str1="123";
    var str2="456";
    var oDiv=document.querySelector("div");
    oDiv.innerText=str1 + str2;
</script>
输出123456
```
```
var s='I/'m a teacher'
斜杠的意思是转译。告诉浏览器里面的单引号是一种符号。
```

### 4.null和undefined
>都表示“无”
null 表示是现在没有值，以后会有。此时null为空
返回值：0
undefined 表示缺少值，就是此处应该有值，但是还没有定义。
返回值：NaN




## 总结
数字number
-Number
-paseFloat
-paseInt
-isNaN

布尔boolean
-Boolean()
-!
-!!
-5个值为假（NaN 0 "" null undefined）其余都为真

字符串string
-将其他数据类型转化为字符串
-字符串拼接 用加号 任何数据类型和字符串拼接的时候，都会默认先转为字符串


## 对象数据类型
       >-对象 object
            -数组类  Array
            -正则类  RegExp
            -数学类  Math
            -对象类  Object
      >-函数  function   

### 对象
>Object是引用数据类型中的对象类，每一个我们使用的具体对象都是这个类的一个实例。

>对象类中的实例都是有键值对组成的（属性名和属性值），键值对是用来描述这个对象特征的。
>数组的索引，相当于对象的属性名，是字符串类型

>**注意**    对象里面也可以是对象，函数等等，不一定是唯一的数据类型

如何创建一个对象实例？
-字面量创建
```
var obj={name:value;
         （字符串类型）name2:value2     
}
```
-实例创建 在该类上创建一个实例
```
var obj=new Object();
```
##### 对象的增 删 改 查
>访问对象 查找
 -对象名.属性名
 -对象名.["属性名"]


>增加键值对（原来没有的属性名）
  -对象名.属性名 = “属性值”
  -对象名["属性名"] = ”属性值“（数字是属性名的时候，只能用这个方法进行获取，并且引号可以忽略不写）

>修改原有属性的属性值
-对象名.属性名 = “新的属性值”
-对象名["属性名"] = ”新的属性值“
>删除
-delete  对象名.属性名(删除整个键值对)
-delete  ["对象名"].属性名(删除整个键值对)
-对象名.属性名 = null（删除属性值，保留属性名）
-对象名["属性名"] = null（删除属性值，保留属性名）

#### 自定义属性

对象中有属性，属性分为内置属性和自定义属性
只要是新增的都是自定义属性
```
obj 
Object {}
__proto__: Object
```
>对象创建后就自带的属性，我们称之为内置属性

>有时候内置属性不能满足我们的需求，我们就可以在这个对象上人为添加一些属性，我们陈志伟自定义属性。

>对象的属性和变量很像，都是用来储存值的容器。

## 函数

>函数是做什么的？
```
JS是从上往下执行代码，有的时候需要定义一个方法，只有特定的条件才会执行这个方法，那么此时我们就需要这些代码，默认时不执行，只有触发时才执行。
函数可以一次定义，多次调用。并且互相不影响
```
|

>如何定义一个函数？
```
关键字 函数名(){
      要执行的js代码块
}
例如：
<script type="text/javascript">
//    alert("加载");
//    定义一个函数，只有点击后才会弹出
//    定义一个容器，将要执行的代码放在这个容器内
//    特定的时候拿出代码执行
    function myClick() {
        alert("加载");
  }
//  function 方法
//  myClick（）  函数名
    var oBtn=document.querySelector("button");
    oBtn.onclick=myClick;


</script>



****************重点*************
函数名后面 没有括号，这个函数名就是一个代表整个函数的变量，用来代表函数和储存函数

函数名后面有括号，代表这个函数已经执行完成的结果,接受到的返回值，此处的返回值如果没有设定，接受值为undefined，如果设定，设定的是什么接收的就是什么。
return 后面的值是什么，返回的就是什么，如果只写return不写值，返回的依然是undefined

函数内return后面的代码不会执行

return后面不管有几个值，只能返回一个值（后面的值）

私有变量：函数内定义的变量，函数外不能够获取到。return只能将变量代表的值返回返回到函数外，变量依然是私有的，谁来接受这个值，函数名（）。
例如：
 function my() {
        var obj={
            name:"123"
        }
    }
    console.log(obj);（获取不到）
```

### 函数的参数
>-形参：就是用来接受实参的变量，用来代表和储存实参
-实参：传入到函数内具体的值

形参和实参是一一对应的关系，如果形参定义，实参没有传，形参返回的是undefined
```
函数定义
function my(形参){
    
}
name(实参)；
函数执行

形参相当只是声明了变量，但没有赋值，传入实参后，形参被赋值。
```

### arguments(相当于实参)
是用来接受实参的一个对象
>接受到的实参放在一个中括号中，每一个实参用逗号分隔开，我们将这个对象接受到的值叫做类数组（中国叫法）
```
 function ar(){
        console.log(arguments);
        (接受到的是[1,2,3,4])
    }
    ar(1,2,3,4)
```
>总结：
 函数用来接受实参的方法：
 - 形参
 - arguments


### JS中的运算符
```
=  赋值  将等号右侧的值赋值给等号左侧
  - +=  x+=y-->x=x+y

== 比较  比较等号左右两侧的值是否相当相等，如果相等返回true  不相等返回false

=== 绝对比较  比较等号两侧的值是否相等，两侧的值需是相同数据类型，如果相等true  不相等false

!= 不等于 a=5 a!=0 条件为真

>  大于

<  小于

>=  大于或者等于

<=  小于或者等于
```
>-逻辑运算符
      -! 取反（非）
      -&&（and）  并且 意思：两个条件同事满足，整体为真。第一个值为假，结束运算，输出第一个值。第一个值为真，就将第二个值输出。
      -| |   或者  意思：两个条件只要有一个满足，整体为真。第一个值为假，直接将第二个值输出出来。第一个值为真，直接将第一个值输出。
      
|
>算数运算符
  -  加  +
  -  减  -
  -  乘  *
  -  除  /
  -  模（求余数） %
  -  ++
  -   -- --