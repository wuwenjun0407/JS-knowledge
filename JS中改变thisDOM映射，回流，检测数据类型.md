# JS中改变thisDOM映射，回流，检测数据类型
## call方法（在低版本IE下不支持）

>函数原型上的call方法是一个函数，这个方法至少要传一个参数，这个参数是用来改变call前面的方法的this的
>**注意：**只有函数的原型上有call这个方法
>call两个作用：
 -   改变this
 -  让当前函数执行

```
fn.call(window)
这里传入window的意思是。
1.将fn的this改为window
2.让fn执行
```
>在非严格模式下，不传参数或者是传了undefined，null,默认是window。**常用**
>call方法从第二个参数开始就是给前面的函数传的参数。fn . call（obj，1，2）
>当使用  . call . call（），两个及以上两个往上的call，如果你传的参数不是一个函数就会报错，因为只有函数的原型上才会有call这个方法。也就是说，你用两个及两个以上的call方法执行的时候，就是相当于把你传进来的函数执行。

|

>在严格模式下（use strict），不传参数或undefined，意思是将this变成了undefined。如果传如的是null，那么this就是null。
>函数执行的时候，前面没有点，this就是undefined。

|
>arguments.callee指向的是函数本身
fn.caller 表示谁调用了这个函数，并输出
this必须是一个对象，如果this是是1，那么this就是Number。这里检测出来是object。因为检测的是this，this必须是对象。
call是一个函数，是定义在Function原型上的函数属性，所有的函数都可以通过_ _proto_ _找到Function原型上的方法。
call在执行的时候里面的this，就是call前面的点之前的东西。
call方法中有个核心的代码就是this（），也就是call前面的函数执行。
```
Function.prototype.call=function () {
    this()
};
function ff() {
    console.log(1);
}
ff.call();//通过ff._ _proto_ _找到所属类的原型Function.prototype
    //找到了这个call方法，ff.call（），call这个执行就是里面的this执行。里面的this就是ff,输出1
```
### call的执行步骤
>两个及两个以上的call（fn，obj，n , m）
 -   fn：必须是函数
 -  obj：是用来改变fn的this
 -  n , m：给fn传的参数


#### call：记住三句话：
        1.改变前面方法的this，不管前面有多少东西
        2.让前面的方法执行，不管前面有多长
        3.call方法最终执行的一句核心是this（）
     外加的：两个及两个以上的call，最后一个call的第一个参数是来改变前面call方法中的this，因为需要这个this执行，所以第一个参数必须是函数，否则会报错     
### 检测代码正确与否
```
try{
     console.log(a);
     var a=1;
     //先执行这里的代码，如果报错了就执行catch里面的代码
} catch（e）{
    //e是一个对象，里面存着错误信息，存在e.message，这里面存折try里面的错误信息
    console.log(e.message);
}
  throw new Error（“我错了”）
```
## apply方法（在低版本IE下不支持）
>apply和call意思和用法一样，区别是：apply第一个参数也是改变this用的，第二个参数是一个数组，这个数组是给前面方法传参数的，将数组里面的每一项一个一个传给函数。

```
function fn(n,m){
    this.n=n+m;
    this.m=n-m;
    return n m
}
fn();
fn.call(null,1,2)
fn.apply(undefined,[1,2])

```

## bind方法（在低版本IE下不支持）
>只改变this返回一个新的函数，原来的函数不变，不让函数执行。bind在以后的时间中常用，我们自己会写一个兼容任何浏览器的方法。
```
var a=2;
function fn(){
   console.log(this.a);
}
var obj={a:1};
fn();//this是window
ff=fn.bind(obj)（）;1
这个ff和fn不是一个函数，ff的this是window，fn的this还是window。
```


### 检测数据类型的方式
>1.typeof  返回值是一个字符串，如果用两个及两个以上的typeof检测的话返回值是“string”，但是他有局限性，能详细检测基本类型，但是null不行，检测出来的是object，对于引用数据类型不能详细检测只有object和function。如果有两个及以上typeof，检测出来就是string
>2.instanceof 检测一个实例是否属于某个类，因为每一种数据类型都对应自己所属的类，所以我们可以通过他来检测数据类型，但是也有局限性，对于基本数据类型，用字面量穿件方式创建的变量检测不出来，构造函数创建方式可以，引用数据类型可以详细检测
>3.类原型上的constructor，每个类的原型（prototype）上都有一个constructor属性，他指向类本身，那么一个具体的数据类型的实例 . constructor。比如：“11” . constructor-->“11” . _ _ proto_ _-->String.prototype,String原型上有constructor指向String本身，也可以通过name属性来得到String类名，也就是他的数据类型。
>console.log（“11”.constructor.name）;-->"toString"
##### 对象Object类的原型上有一个toString,他可以检测数据类型，那么我们就调用Object . prototype.toString()这个方法，用call将里面的this改变成我想检测的那个数据
```
var ary=[1,2];
console.log(Object.prototype.toString.call(ary));
输出：[object Array]
```
>利用toString方法检测数组，返回Array的方法
```
function getType(type) {
    return Object.prototype.toString.call(type).split(" ")[1].replace("]",'');
}
var ary=[1,2];
console.log(getType(ary));
输出：Array
```

### try.catch
>try里面的代码，如果报错了，就会执行catch里面的代码，错误信息会存储在catch的e中。

### 将类数组转为数组的方法
```
第一种：
function toArray(likeArray) {
    var ary=[];
    for(var i=0;i<likeArray.length;i++){
        ary.push(likeArray[i])
    }
    return ary;
};

第二种：
function ff() {
    //arguments 参数集合类数组
    return toArray(arguments);
};
ff(1,2,3,4)

第三种：解决兼容性的问题
function toArray(likeArray) {
    try{
        return [].slice.call(likeArray);
    }catch(e){
        var ary=[];
        for(var i=0;i<likeArray.length;i++){
            ary.push(likeArray[i])
        }
        return ary;
    }
 
};
```
### 一个数组求最大值或最小值
```
最大值：
var ary=[3,5,1,24,19,10,57];
var max=Math.max.apply(null,ary);
console.log(max);

最小值：
var ary=[3,5,1,24,19,10,57];
var min=Math.min.apply(null,ary);
console.log(max);
```
### 数组求平均值
```

```

## json
>json是一个对象，是window下的一个属性，也可以理解为是一个全局变量，在低版本IE下没有这个对象
>json不是一个单独的数据类型，只是一个特殊的数据格式
>json 对象和普通对象的区别
-   json属性名用双引号包起来
-  属性值是字符串的话也用双引号包起来

```
var obj={a:"a",1:1};
普通的对象

var jsonObj={"a":"a","1":1,"age":12,"ary":[1,2]}
json对象

var jsonStr='{"a":"a","1":1,"age":12,"ary":[1,2]}'
json字符串，一般从后台获取回来的数据都是json字符串
```
#### 将json格式的字符串转化为json格式的对象
```
console.log(JSON.parse(jsonStr));
JSON必须是大写
```
#### 将json格式的对象转化为json格式的字符串
```
console.log(JSON.stringify(jsonObj));
```
>如果IE低版本下没有就用eval来实现

##### 在IE低版本下兼容的json方法

```
第一种：
function jsonparse(jsonStr){
       try{
      //如果浏览器中有JSON就用这里的
      return JSON.parse(jsonStr)
    }catch(e){
      //浏览器里面没有就用这里的
      return eval("("+jsonStr+")")
    }
}
第二种:
function jsonparse(jsonStr){
     return "JSON" in window?JSON.parse(jsonStr):eval("("+jsonStr+")")
}
```

## DOM映射
>通过DOM方法获取的一个元素集合（类数组），这个集合仍然和页面的元素保持联系，并且这个元素集合会随着页面元素的增加而增加，j减少而较少。即使把这个类数组转为一个数组，每个元素仍然和这个压面有联系。这就叫做DOM映射。

## 回流
>元素的位置发生改变（增加元素，删除元素，移动元素）这样的话就会引起回流，让整个页面重新渲染一遍（加载）从而造成了性能的浪费

# 重绘
>元素的样式发生改变，就会把当前的这个元素重新渲染一遍。
**注意：**在以后的项目中，能用重绘代替就不用回流，能用一次回流就不要使用多次。

## 向页面增加元素的方式
>方法：
-   1.动态创建的方式   document.createElement,然后一个一个appendChild，会造成多次回流，这样不好，但是他有个好处是不会改变原来元素（比如他不会影响之前绑定的事件）
-   2.通过拼接字符串，最后在一次性通过innerHTML，这样只会引起一次回流，比较好，但是，他会改变原来的元素（比如会影响他之前绑定的事件）
-  3.文档碎片（好用），他就是一个容器专门来盛放DOM元素的（文档碎片的容器：document . createDocumentFragment（））

|

>文档碎片的步骤：
-  1.先创建元素（var oli=document.createElement("li")）
-  2.按需求给元素增加一些需要的属性
-  3.暂时存放在flg(DOM碎片)中，也是appendChild进去的
-  4.循环完之后，把整个flg放到ul中，news.appendChild（flg）,这样只会引起回流一次
