# JS盒子模型

>css盒子模型：margin，border，padding，height/width
JS盒子模型：JS提供了一系列的方法来获取css盒子模型中的相关属性
### 关于JS获取css样式元素的信息
>height：加入给元素设置了height，不管内容多少，你获取出来的都是设置的高度，如果没有设置高度，获取出来的height就是真实内容的高度。
### JS盒子模型13个方法


----------
![Alt text](./QQ截图20170509101629.png)


>1.client系列
-   clientWidth：内容宽+左右padding //260
-  clientHeight：内容高+上下padding //260
-  clientLeft：左边框的宽度 //20
-  clientTop：上边框的宽度 //20

>2.offset系列
-   offsetWidth：clientWidth+左右border //300
-  offsetHeight：clientHeight+上下border //300
-  offsetParent：父级参照物 //可以直接用这个获取
-  offsetLeft：左偏移量：当前元素外边框距离父级参照物（offsetParent）的内边框的水平距离 //100
-  offsetTop：上偏移量：当前元素上边框距离父级参照物（offsetParent）的上边框的垂直距离 //100
-  在IE8下offsetLeft：左偏移量+父元素自己的左border
-  在IE8下 offsetTop：上偏移量+父元素自己的上
-  border
#### offsetParent查找方法
-  offsetParent：当前元素的父级参照物，从父级元素往上找，找到一个被定位（relative，absolute，fixed）元素，就是当前元素的offsetParet，如果一直找到body都没有定位元素，那么他的offsetParent就是body。

>3.scroll系列
-   scrollWidth：有溢出的情况下就是内容宽+左padding（没有溢出的情况和clientWidth）
-  scrollHeight：有溢出的情况下就是内容高+上padding（没有溢出的情况和clientHeight）
-  scrollLeft：内容区域滚动条卷去的宽度
-  scrollTop：内容区域滚动条卷取的高度

>**注意1：**这十三个盒子模型属性只有scrollLeft和scrollTop是可以修改值的。最小值是0；就算你给他设置了一个负数，他的值也是0。其他的只能读取不能赋值，给他们赋值也不起作用。
>**注意2：**这十三个盒子模型属性获取的值都是整数，是浏览器默认四舍五入。

#### 获取当前元素到body的距离（针对有定位的）
```
  //offset(curEle),求curEle和body的上偏移量和左偏移量
   //当一个函数最终得到多个值那么你就让他返回一个对象就可以了
   //注意：在IE8中，左偏移量和上偏移量包括offsetParent（父级元素的边框）。
   function offset(curEle) {
       //形参curEle:当前的元素
       if(window.navigator.userAgent.indexof("MSIE 8")===-1){
        //如果当前浏览器不是IE8的时候，执行这里面的
        curL+=par.clientLeft;//当前元素的左偏移量加上左边框
        curT+=par.clientTop//当前元素的上偏移量加上上边框
      }
       var curL=curEle.offsetLeft;//获取当前元素的左偏移量
       var curT=curEle.offsetTop;//获取当前元素的上偏移量
       var par=curEle.offsetParent;//获取当前元素的父级元素
       while (par){//循环
           
           curL+=par.offsetLeft;//当前元素的左外边框到父级元素的左内边框的距离
         
           curT+=par.offsetTop;//当前元素的上外边框到父级元素的上内边框的距离
           par=par.offsetParent;//继续获取下一个父级元素
       }
       return{
           left:curL,
           top:curT
       }
   }
   offset(inner).left
```
## 获取浏览器宽高的方法
```
    function win(attr,value) {
        //如果只传一个参数，说明是要获取浏览器的属性值
        //如果传两个值是想设置属性的值：screenTop/screenLeft这两个值才会用到value
        if(typeof value=="undefined"){
            return document.documentElement[attr]||document.body[attr]
        }else {
            document.documentElement[attr]=value;
            document.body[attr]=value;
        }
    }
    console.log(win("scrollTop"));
    console.log(win("clientLeft"));
```
### onscroll事件
>onscroll事件：只要滚动条位置发生改变就会触发这个事件
```
box.onscroll=function () {
        console.log(box.scrollTop);
    }
```