# JS中this的五种方法
### 在非严格模式下
>1. 自执行函数的this永远是window
>2. 给元素绑定方法，给谁绑定this就是谁
>3. 方法执行，看方法前面是否有” . “,前面是谁this就是谁，没有的话就是window
>4. 在构造函数中，函数体中的this . xxx=xxx中的this就是当前类的实例
>5. 使用call或者apply来改变this的指向。**注意：**一旦遇到call或者apply上述的四条都没用了


### 严格模式下
>严格模式的写法。
```
"use strict"
写在整个js文件的开头
```
>自执行函数的this永远是undefined
>方法执行，看方法前面是否有” . “，有的话点前面是谁this就是谁，没有点的话this就是undefined
```
fn.call(null,1,2);
fn.apply(undefined,[1,2]);
call();this是undefined；
fn.call();this 是undefined；
call(null);this 是null；
fn.call(null);this是null；
call(undefined);this undefined；
fn.call(undefined);this是undefined；
```

### 严格模式和非严格模式下的this区别
>对于js代码中没有写执行主体的情况下，非严格模式下默认都是window执行的，所以this指向的是window，但在严格模式下，没有写就是没有执行主体，this指向的是undefined。