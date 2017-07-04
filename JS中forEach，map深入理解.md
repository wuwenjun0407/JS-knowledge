# JS中forEach，map深入理解
>forEach是异步的，一般通过参数传进去执行的都是回调函数，是异步的。
```
 var ary=[1,2,3,4];
    //forEach(function(){},that);
    //function(){默认的this是window}；
    //that 就是用来改变这个函数中的this的，不传的话就是window
    ary.forEach(function (item,index,input) {
        //this===window;默认的情况，就是没有传
        //this===ary;  改了之后 
        console.log(this);
```
>模拟forEach的实现原理
```
 Array.prototype.each=function (fn,that) {
        //fn是个函数，that用来改变fn执行时候里面this的
        //fn要执行多少次？要看那个执行each方法的数组实例有几项
        //实例：this
        //that穿了就用你传的，不传就是window
        that=that||window;
        for(var i=0;i<this.length;i++){
            fn.call(that,this[i],i,this)
        }
    };
    ary.each(function(){},ary);
```
### map深入理解
>map 有返回值，每一次执行返回值组成一个新数组返回来
```
 ary.map(function (item,index,input) {
        return 1;
    },that  );
    console.log(ary1);//[1,1,1,1]
```
>模拟map的实现原理
```
 ary.prototype.forMap=function (callback,that) {
        that=that||window;
        var ary=[];
        for(var i=0;i<this.length;i++){
            var res=callback.call(that,this[i],i,this);
            ary.push(res);
        }
        return ary;
    }
```