# JS DOM获取元素
>DOM是Doument Object model（文档对象模型）的缩写
>DOM可以操作元素以及元素的内容，标签属性，文字，音频视频等等。（只要是直接写在文档中的，DOM都可以操作），引入到HTML里面的不能直接操作。
>DOM可以描述每个元素之间的关系图谱，例如xxx的父元素，xxx的子元素等。

## DOM获取元素的方法


### 通过选择器选择
>-  querySelect("value")通过选择器获取元素
  -   传入的valuea值与css选择器相同，可以写类，ID，标签，后代选择器，子代选择器。
  -   IE低版本浏览器不兼容（IE6 7 8）
 - 获取方式如下：
```
 var oDiv=document.querySelector("div")
```
### 通过选择器获取
>   -  querySelectAll("value")通过选择器获取父元素下同类型所有元素
    - 获取方式如下：
```
 var oDiv=document.querySelectorAll("div")
```
### 通过ID名获取
>> 通过ID名获取，获取的是一个元素,一般浏览器中一个页面相同的ID只有一个，所以获取出来的是一个元素，但是以后可能或遇到有相同的情况，这样获取的是第一个,这就要求我们起名的时候相同的ID只能一个。
>
  - 获取方式如下：
```
      [上下文].getElementById("元素的Id");
```   
>注意：通过ID获取元素，上下文只能是document。
>在IE下，name的作用和ID 一样，所以name的值和ID的值不能一样，只有input的name值是有效果的，其他的name值识别不到。
```
<input type="text" name="123">
```

### 通过name来获取
  >通过元素name属性的属性值获取一组元素（类数组，有length，索引）
  >获取出来的是类数组
  >多用在表单元素上
>
   - 获取方式如下：
     
```
      [上下文].getElementsByName("name名字");
```   
### 通过class名来获取
>  通过class名获取一组元素（类数组，有length，索引）
>注意：[上下文]自己定义，一般都是他的父亲，最多不超过三级。后面必须加索引，否则获取出来的是一组。
>在IE67中没有这个属性和方法
  - 获取方式如下：
  
```
      [上下文].getElementsByClassName("class名")[0]（索引）;
      var cur=list[0]（获取这个集合的第一个元素）
```  
### 通过标签名获取
>4)   通过标签名获取一组元素（类数组，有length，索引） 
  - 获取方式如下：
  
```
      [上下文].getElementsByTagName("标签名");
```  

### 获取元素的样式
>元素（对象）有个内置属性叫style，style属性也是一个对象他有很多的样式属性。元素.style：color；
>|
>|
>  下面的方法只能获取，不能许改。
>  原因：怕被随意篡改。
>  可以获取外链式或者内嵌式。
>  IE678不兼容。他有自己的方法：currentstyle 
```
  getComputedStyle(元素).样式属性(color)             获取所有的样式（只能获取不能修改）
```  
>**注意**style只能获取行内样式（不常用），添加样式也是在行内（常用）
|
|
添加和获取样式如下：

```
  var div2=document.getElementById("div1");
   console.log(div2.style.width);
    div2.style.color="red"
```
### 获取文档的根元素元素
```
doucument.doucumentElement
```
###  获取body元素
```
doucument.body
```
### 获取根元素的宽度
```
    var w=document.documentElement.clientWidth||document.body.clientWidth;
```
### 获取根元素的高度
```
    var d=document.documentElement.clientHeight||document.body.clientHeight;
```


## DOM节点与关系属性

>节点：Node在页面中出现的所有东西都是节点，元素，注释，文本等都是节点。（返回值都是类数组）
>//元素节点
    //  节点：在HTML中出现的所有东西都是节点
    //nodeName nodeType nodeValue
    //1 元素节点
    //nodeName:大写的标签
    //nodeType  1
    //nodeValue null
    // 2.文本节点
    //nodeName #text
    //nodeType  3
    //nodeValue  文本内容
    // 3.注释节点
    //nodeName:#comment
    //nodeType  8
    //nodeValue  注释内容
    // 4.document.
    //nodeName  #document
    //nodeType  9
    //nodeValue  null

|
>获取元素下所有的子节点(childNodes)
>兼容所有浏览器
语法：
```
var ul=document.getElementsByTagName("ul");
var nodes=ul.childNodes;
console.log(nodes)
```
>获取指定元素下所有的元素子节点（IE8以下不兼容）（xxx.children）
>
>获取指定元素的父节点（xxx.parentNode）肯定是元素节点
>
>获取指定元素的上一个哥哥节点
>兼容所有浏览器
xxx.previousSibling)0
>
>获取指定元素的上一个哥哥元素节点(xxx.previousElementSibling)不兼容IE8以下
>
>获取指定元素的下一个弟弟节点 兼容所有浏览器(xxx.nextSibling)0
>
>获取指定元素的下一个弟弟元素节点（xxx.nextElementSibling）IE678不兼容
>
>获取指定元素下的第一个节点（xxx.firstChild）不兼容
>
>获取指定元素下的第一个元素节点（xxx.firstElementChild）不兼容
>
>获取指定元素下的最后一个节点（xxx.lastChild）不兼容

>获取指定元素下的最后一个元素节点（xxx.lastElementChild）不兼容

```
处理兼容问题的方法：（获取上一个哥哥的元素节点）
function pre(curEle){
    if("previousElementSibling" in curEle){
    return curEle.previousElementSibling
}else{
//  先找一个哥哥节点，存在并且不是元素节点的话就继续往上找
    var pre=curEle.previousSibling;
    while(pre && pre.nodeType!==1){
         pre=pre.previousSibling;
}
return pre;
}
}
```


### DOM的增 删 改 查及应用

#### 创建元素节点createElement（）
  -   向指定元素所有内容之后 添加一个元素节点
**语法**：
```
父级元素.appendChild(新创建的元素节点)
```

>**注意**：通过createElement创建的元素节点，不能通过innerHTML添加到页面上

|
>-   向指定元素之前添加新创建的元素节点
**语法：**
```
parent.insertBefore(新创建的元素,新创建元素后面的元素，)
```


### 删除创建的元素节点
**语法：**
```
parent.removeChild("需要移出的元素")
```

### 克隆元素节点
**语法：**
```
要克隆的元素节点.cloneNode(true)
```
>false（或者不填） 默认 只克隆当前元素，里面的内容不会复制
true 将这个元素及里面的内容克隆一份

### 替换元素节点
**语法：**
```
父级元素.replaceChild(替换的元素对象，被替换的元素对象)
```

### 创建属性节点（会添加到元素的开始标签内）
**语法：**
```
元素.setAttribute('属性名'，'属性值')
```
>只能通过getAttribute('属性名')；获取属性节点
>只能通过removeAttribute('属性名')；删除属性节点


## Math数学类

>作用：执行常见的算数任务
>   1、Math.abs() 取绝对值
    2、Math.ceil()向上取整 （出现小数点就向上＋1）
    3、Math.floor()向下取整
    4、Math.round()四舍五入
    5、Math.max(val1,val2,val3...)取最大值
    6、Math.min(val1,val2,val3...)取最小值
    7、Math.random()获取[0-1)之间的随机小数（不包含1）
    8、Math.round(Math.random()*(m-n)+n) 获取任意两个数之间的随机数，获取n-m之间的随机整数，包含n和m。
    
    取随机数的方法：
```
 function getNum(n,m) {
        if(n>m){
            var temp=n;
            n=m;
            m=temp;
        }
        var str="";
        for(var i=0;i<4;i++){
            str+=Math.round(Math.random()*(m-n)+n);
        }
        document.write(str);
    }
    getNum(1,8);
```
    += 是在原有基础上进行累加




