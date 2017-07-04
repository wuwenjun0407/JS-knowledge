# JS中DOM2级事件的兼容问题

### 在标准浏览器中，用DOM2级事件绑定
>**注意1：**如果给同一个事件行为绑定多个函数，都会触发，而且是按照顺序执行的。
>**注意2：**给同一个事件行为，同一个函数，同一个阶段，不能重复绑定，只会执行一个。
>**注意3：**绑定的那个函数中的this仍然是被绑定的元素。
### 在IE6-8中的DOM2级
>在低版本绑定DOM2级的方法：
```
box.attachEvent("onclick")//需要加上on
```
>移除事件：detachEvent
>**注意1：**事件类型需要在前加上”on”：“onclick”
>**注意2：**不能设置发生的阶段，都是在冒泡阶段发生的
>**注意3：**同一个事件行为，同一个函数，能够多次绑定
>**注意4：**给同一个事件行为，绑定多个函数，执行顺序混乱
>**注意5：**绑定的那个函数执行的时候里面的this是window

### DOM2级事件绑定兼容写法
>绑定on
```
function on(ele,type,callBack) {
        //ele 绑定事件的元素 type  事件类型  callBack  绑定的函数
        //先判断当前浏览器中有没有addEventListener这个属性，有的话就用这个。没
        if(ele.addEventListener){
            ele.addEventListener(type,callBack,false);
            //有的话，就用attachEvent，注意第一个参数，事件类型中要加上“on”；
        }else {
            //因为callBack在执行的时候，this是window，我们要把他的this变成ele，所以我们把callBack函数用一个函数保起来，在这个函数中通过call（）让callBack的this改变ele，让callBack执行。
            function run() {
                callBack.call(ele)
            };
            ele.attachEvent("on"+type,run)
        }
    }
```
>移除off
```
function off(ele,type,callBack) {
        if(ele.removeEvent){
            ele.removeEvent(type,callBack);
        }else {
            ele.detachEvent("on"+type,callBack)
        }
    }
```
>阻止IE下同一个函数，同一个事件，多次执行的问题
```
 function on(ele,type,callBack) {
            if(ele.addEventListener){
                ele.addEventListener(type,callBack)
            }else {
                //每个事件类型都准备一个数组，放到当前这个元素的自定义属性上
                if(!ele["event"+type]){
                    //每一次进来先判断呢之前有没有这个类型的小数组,没有的话先创建一个。
                    ele["event"+type]=[];
                }
                //将这个事件类型的小数字获取出来，向里面添加你传进来的函数callBack
                var events=ele["event"+type];
                //放之前先判断这个小数组中有没有callBack,如果有了就直接return，后面就不用绑定了
                if(events&&events.length){
                    for(var i=0;i<events.length;i++){
                        if(events[i]===callBack){
                            return;
                        }
                    }
                }
                events.push(callBack);
                function run() {
                    callBack.call(ele)
                }
                ele.attachEvent("on"+type,run);
            }
        }
```
>删除绑定事件的方法
```
function off(ele,type,callBack) {
        if(ele.removeEventListener){
            ele.removeEventListener(type,callBack);
        }else {
            //获取除对应事件类型的小数组
            var events=ele["event"+type];
            if(events&&events.length){
                //循环数组中的每一项找到callBack 删除
                for(var i=0;i<events.length;i++){
                    if(events[i]===callBack){
                        ele.detachEvent("on"+type);
                        //删除小数组中的那个callBack
                        events.splice(i,1);
                        break;
                    }
                }
            }
        }
    }
```
### this指向问题
>问题:
>在低版本浏览器中绑定的事件函数中的this默认指向的是window,在高版本浏览器中this指向的是当前绑定的那个元素,所以要把this统一变成指向绑定的元素
>解决:
>在事件绑定中,将callback放到另一个run函数中包起来,在run函数中利用call函数将callback中的this变成当前绑定事件的元素ele,再让callback函数执行,最后将run函数绑定给当前元素,当触发事件行为的时候,就会让run函数执行,run函数一执行就是里面的callback执行
### 同一个函数类型,多次重复绑定同一个函数
>问题:
>在低版本浏览器中给同一个事件行为可以多次绑定同一个函数,但是在高版本浏览器中同一个事件行为,同一个函数只能绑定一次,在实际操作中只需要执行一次就够了,所以要处理低版本浏览器的多次重复绑定问题
>解决:
>在绑定之前先看看当前元素中有没有对应事件类型的小数组,如果没有先创建一个这个类型的小数组"event"+type,获取小数组并循环每一项看看里面有没有这个callback函数,如果有就直接return不用绑定了,没有的循环就直接执行完成后,把这个callback放到当前这个小数组中

### 处理全部兼容
```
    function on(ele,type,callBack,bool) {
        bool=bool||false;
        if(ele.addEventListener){
            ele.addEventListener(type,callBack,bool)
        }else {
            if(!ele["event"+type]){
                ele["event"+type]=[];
                ele.attachEvent("on"+type,function (e) {
                var e=window.event;
                run.call(e)
            });
            }
            var events=ele["event"+type];
            if(events&&events.length){
                for(var i=0;i<events.length;i++){
                    if(events[i]===callBack){
                        return;
                    }
                }
            }
            events.push(callBack);
            
        }
    }
    function off(ele,type,callBack,bool) {
        bool=bool||false;
        if(ele.removeEventListener){
            ele.removeEventListener(type,callBack,bool)
        }else {
            var events=ele["event"+type];
            if(events&&events.length){
                for(var i=0;i<events.length;i++){
                    if(events[i]===callBack){
                        ele.detachEvent("on"+type,callBack);
                        events.splice(i,);
                        break;
                    }
                }
            }
        }
    }
    function run(e) {
        //事件对象一些属性的不兼容问题
        e.target=e.target||e.srcElement;
        e.preventDefault=function () {
            e.returnValue=false;
        };
        e.stopPropagation=function () {
            e.cancelBubble=true;
        };
        e.pageX=(document.documentElement.scrollLeft||document.body.scrollLeft)+e.clientX;
        e.pageY=(document.documentElement.scrollTop||document.body.scrollTop)+e.clientY;
        var events=this["event"+e.type];
        if(events&&events.length){
            for(var i=0;i<events.length;i++){
                events[i].call(this,e)
            }
        }
    }
```
