# JS中onload事件

### DOM0级事件    只能写一次
```
window.onload=function () {
    页面上所有的东西都加载完成（DOM，音频，视频，CSS，外部引入的文件，图片。。）才开始执行里面的代码
}
```
### DOM2级事件可以实现多次绑定
```
  window.addEventListener("load",function () {

    },false);
```
### jQuery 写法
```
 $(document).ready(function () {
      //只要页面上所有的DOM结构（包括图片）加载完成后才开始执行
    });
    jQuery(function ($) {
        
    });
    $(function () {
        
    });
```
### window下的写法
```
document.addEventListener("DOMContentLoaded",function(){},false);
```

### 兼容写法
```
 function DOMLoad(fn) {
        if(document.addEventListener){
            document.addEventListener("DOMContentLoaded",fn,false);
        }else {
            //当压面的状态发生改变的时候，我们可以通过document.readyState来监听页面的变化
            /*
            0-uninitialized XML对象被产生，但是没有任何文件被加载
            1-loading  加载程序进行中，但是文件尚未开始解析
            2-loaded   部分文件被加载解析，但是对象模型尚未建成
            3-interactive  仅仅堆部分已经加载的文件有效，但是文档模型建成了，只能是只读的
            4-completed   文件加载完成，加载成功
             */
            document.onreadystatechange=function () {
                if(document.readyState==="completed"){
                    fn();
                }
            }
        }
    }
```