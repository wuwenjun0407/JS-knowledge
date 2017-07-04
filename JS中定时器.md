# JS中定时器


## 定时器

### 定时器的作用
>想要一个方法按照指定的时间重复执行，或指定一个时间只执行一次，这个时候，就需要定时器
### 定时器的分类.
>定时器是一个全局函数，里面需要传入两个参数。
>第一个参数是一个函数（就是你要执行的那个函数
>第二个参数是时间（过多久执行一次，或多次执行）时间参数都是以毫秒为单位，一秒等于1000毫秒
>定时器是windows的方法，所以可以省略windows。
>Windows.setIntreval([function(){},[interval])
-  指定一个时间，每间隔这个时间，都会执行这个方法
>
>windo.setTimeout([function(){}],[interval])
-   指定一个时间，到达这个时间方法执行一次，就不会在执行了

>定时器的返回值是一个数字，代表我是第几个定时器，这里不区分setIntreval，setTimeout。


### 清除定时器（将定时器停止）
>用什么定时器，都可以人选下面一种方法清除。
-   clearTimeout
-   clearInterval

```
var timer=window.setTimeout(function(){
    console.log("1")
},1000)

timer=1  time就是一个变量里面存了一个值是1

window。clearTimeout(1) 
清除定时器不是把定时器破坏，而是把里面的方法阻止了，结果是：
timer=null；
```

### 引用数据类型的赋值

```
var obj={aa:"aa"}

1.浏览器先要判断一下赋值是什么数据类型
2.引用数据类型的话，浏览器先要开辟一个堆内存，将里面的值存起来
3.将地址赋值给变量名

```