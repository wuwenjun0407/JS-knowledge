# JS中常用的封装方法
```

var public=(
    function(){
        //1.将类数组转为数组
        function toArray(likeArray){
            var ary=[];
            try{
                return ary.slice.call(likeArray)
            }catch(e){
                for(var i=0;i<likeArray.length;i++){
                    ary.push(likeArray[i])
                }
                return ary;
            }
        };
        //2.将JSON字符串转为JSON对象
        function toJsonObj(jsonstr){
            try{
                return JSON.parse(jsonstr)
            }catch(e){
                return eval("("+jsonstr+")")
            }
        }
        //3.求当前元素距离body的偏移量
        function offset(curEle){
            var L=curEle.offsetLeft;
            var T=curEle.offsetTop;
            var P=curEle.offsetParent;
            while(P){
                if(window.navigator.userAgent.indexOf("MSIE 8")==-1){
                    L+= P.clientLeft;
                    T+= P.clientTop;
                }
                L+= P.offsetLeft;
                T+= P.offsetTop;
                P= P.offsetParent;
            }
            return {left:L, top:T}
        }
        //4.获取或者设置当前浏览器的盒子模型属性I下只能用body获取
        function win(attr,value){
            if(typeof value=="undefined"){
                return document.documentElement[attr]||document.body[attr];
            }else{
                document.documentElement[attr]=value;
                document.body[attr]=value;
            }
        }
        //5.获取随机数的方法
        function getRandom(n,m){
            n=Number(n);
            m=Number(m);
            if(isNaN(n)||isNaN(m)){
                return Math.random();
            }
            if(n>m){
                //n=n+m;
                //m=n-m;
                //n=n-m;
                var c=n;
                n=m;
                m=c;
                c=null;
            }
            return Math.round(Math.random()*(m-n)+n);
        }
        //6.获取元素的样式属性值
        function getCss(curEle,attr){
            var val=null;
            if("getComputedStyle" in window){
                val=window.getComputedStyle(curEle)[attr];
            }else{
                if(attr=="opacity"){
                    //filter:alpha(opacity=35.7);
                    val=curEle.currentStyle["filter"];
                    var reg1=/^alpha\(opacity=(\d+(?:\.\d+)?)\)$/;
                    val=reg1.test(val)?RegExp.$1/100:1;
                }else{
                    val=curEle.currentStyle[attr] ;
                }
            }
            var reg2=/^-?\d+(?:\.\d+)?(?:px|pt|pp|rem|em|deg)?$/g;
            if(reg2.test(val)){
                val=parseFloat(val);
            }
            return val;
        }
        //7.设置元素的样式属性
        function setCss(ele,attr,val){
            if(attr=="opacity"){
                ele.style.opacity=val;
                ele.style.filter="alpha(opacity="+val*100+")";
                return ;
            }
            if(attr=="float"){
                ele.style.cssFloat=val;
                ele.style.styleFloat=val;
            }
            var reg=/^(width|height|top|bottom|right|left|(margin|padding)(Top|Bottom|Right|Left)?)$/;
            if(reg.test(attr)&&!isNaN(val)){
                val+="px";
            }
            ele.style[attr]=val;
        }
        //8.批量设置元素的样式属性
        function setGroupCss(ele,obj){
            obj=obj||[];
            if(obj.toString()=="[object Object]"){
                for(var key in obj){
                    this.setCss(ele,key,obj[key])
                }
            }
        }
        
  //9.根据参数的不同选择不同的方法
        function css() {
            if(arguments.length==3){
                setCss.apply(this,arguments);
                return;
            }
            if(arguments.length==2){
                if(arguments[1].toString()=="[object Object]"){
                    setGroupCss.apply(this,arguments);
                    return;
                }else {
                    return getCss.apply(this,arguments)
                }
            }
        }
        //10.prev获取上一个哥哥元素节点
        function prev(curEle) {
            if(standardBrowser){
                return curEle.previousElementSibling;
            }
            var pre=curEle.previousElementSibling;
            while (pre&&pre.nodeType!==1){
                pre=pre.previousElementSibling;
            }
            return pre;
        }
        //11.next获取下一个弟弟元素节点
        function next(curEle) {
            if(standardBrowser){
                return curEle.nextElementSibling;
            }
            var nex=curEle.nextElementSibling;
            while (nex&&nex.nodeType!==1){
                nex=nex.nextElementSibling;
            }
            return nex;
        }
        //12.prevAll获取所有的哥哥元素，返回一个数组
        function prevAll(curEle) {
            var prevAry=[];
            var pre=this.prev(curEle);
            while (pre){
                prevAry.unshift(pre);
                pre=this.prev(pre);
            }
            return  prevAry;
        }
        //13.nextAll获取所有的弟弟元素返回一个数组
        function nextAll(curEle) {
            var nextAry=[];
            var nex=this.next(curEle);
            while (nex){
                nextAry.push(nex);
                nex=this.next(nex)
            }
            return nextAry;
        }
        //14.sibLing 获取当前元素相邻的两个兄弟,返回一个数组
        function sibLing(curEle) {
            var sibAry=[];
            var pre=this.prev(curEle);
            var nex=this.next(curEle);
            pre?sibAry.push(pre):void 0;
            nex?sibAry.push(nex):void 0;
            return sibAry;
        }
        //15.sibLings 获取当前元素的所有兄弟，返回一个数组
        function sibLings(curEle) {
            return this.prevAll(curEle).concat(this.nextAll(curEle));
        }
        //16.index 获取当前元素的索引
        function index(curEle) {
            return this.prevAll(curEle).length;
        }
        //17.获取当前元素指定标签名的孩子元素节点
        function children(curEle,tagName) {
            var kids=curEle.childNodes;//当前元素所有的孩子节点
            var kidsAry=[];
            for(var i=0;i<kids.length;i++){
                if(kids[i].nodeType===1){
                    if(typeof tagName!=="undefined"){
                        if(kids[i].nodeName==tagName.toUpperCase()){
                            kidsAry.push(kids[i]);
                            continue;
                        }
                    }
                    kidsAry.push(kids[i])
                }
            }
        }
        //18.获取当前元素第一个元素子节点
        function firstChild(curEle) {
            if(standardBrowser){
                return curEle.firstElementChild;
            }
            var firstKids=curEle.firstChild;
            while (firstKids&&firstKids.nodeType!==1){
                firstKids=firstKids.nextSibling;
            }
            return firstKids;
        }
        //19.获取当前元素最后一个元素子节点
        function lastChild(curEle) {
            if(standardBrowser){
                return curEle.firstElementChild;
            }
            var lastKids=curEle.lastChild;
            while (lastKids&&lastKids.nodeType!==1){
                lastKids=lastKids.previousSibling;
            }
            return lastKids;
        }
        //20.判断当前元素有没有某个或者某些class名
        function hasClass(curEle,classStr) {
            var reg=new RegExp("(^| +)"+classStr+"( +|$)");
            return reg.test(curEle.className)
        }
        //21.给元素增加class名
       /* function addClass(curEle,classStr) {
            //1.处理classStr将其首位空格去掉
            classStr=classStr.replace(/^ +| +$/g,"");
            //2.将classStr中间出现的多个空格，都变成一个
            classStr=classStr.replace(/ +/g," ");
            //3.判断curEle之前有没有className
            if(curEle.className.length>0){
                //有的话，先加一个空格在拼接上classStr
                curEle.className+=" "+classStr;
            }else {
                //没有的话直接赋值
                curEle.className=classStr;
            }
        }*/
        //21.给元素增加class名
        function addClass(curEle,classStr) {
            //1.处理classStr将其首位空格去掉
            classStr=classStr.replace(/^ +| +$/g,"");
            //2.按照一到多个空格将classStr拆分成数组
            var classAry=classStr.split(/ +/g);
            //3.循环数组，判断curEle之前的className中有没有那个类名，没有的话给他加上
            for(var i=0;i<classAry.length;i++){
                if(!this.hasClass(curEle,classAry[i])){
                    curEle.className+=" "+classAry[i];
                }
            }
            //4.为了保证第一个前面没有空格，在做一次首位空格去掉
            curEle.className=curEle.className.replace(/^ +| +$/g,"");

        }
        //22.给元素删除class名
        function removeClass(curEle,classStr) {
            //1.处理classStr将其首位空格去掉,然后拆分为数组（按照一到多个空格）
            classStr=classStr.replace(/^ +| +$/g,"").split(/ +/g);
            //2.循环判断之前的class中有没有，有的话替换成空字符串
            for(var i=0;i<classStr.length;i++){
                var reg=new RegExp("(^| +)"+classStr[i]+"( +|$)");
                curEle.className=curEle.className.replace(reg,"");
            }
            //3.最后再把首尾空格去掉
            curEle.className=curEle.className.replace(/^ +| +$/g, "");
        }
        //23.判断当前元素的如果有传进去的类名就删除，没有就增加
        function toggleClass(curEle,classStr) {
            classStr=classStr.replace(/^ +| +$/g,"").split(/ +/g);
            for(var i=0;i<classStr.length;i++){
                this.hasClass(curEle,classStr[i])?this.removeClass(curEle,classStr[i]):this.addClass(curEle,classStr[i])

            }
        }


        return{
            toArray:toArray,    //1.将类数组转为数组
            toJsonObj:toJsonObj, //2.将JSON字符串转为JSON对象
            offset:offset,//3.求当前元素距离body的偏移量
            win:win,//4.获取或者设置当前浏览器的盒子模型属性（）就是一屏的高度
            getRandom:getRandom,   //5.获取随机数的方法
            getCss:getCss,//6.获取元素的样式属性值
            setCss:setCss,//7.设置元素的样式属性
            setGroupCss:setGroupCss,//8.批量设置元素的样式属性
            css:css,//9.根据参数的不同选择不同的方法
            prev:prev,//10.prev获取上一个哥哥元素节点
            next:next,//11.next获取下一个弟弟元素节点
            prevAll:prevAll,//12.prevAll获取所有的哥哥元素，返回一个数组
            nextAll:nextAll,//13.nextAll获取所有的弟弟元素返回一个数组
            sibLing:sibLing,//14.sibLing 获取当前元素相邻的两个兄弟,返回一个数组
            sibLings:sibLings,//15.sibLings 获取当前元素的所有兄弟，返回一个数组
            index:index,//16.index 获取当前元素的索引
            children:children,//17.获取当前元素指定标签名的孩子元素节点
            firstChild:firstChild,//18.获取当前元素第一个元素子节点
            lastChild:lastChild,//19.获取当前元素最后一个元素子节点
            hasClass:hasClass,//20.判断当前元素有没有某个或者某些class名
            addClass:addClass,//21.给元素增加class名
            removeClass:removeClass,//22.给元素删除class名
            toggleClass:toggleClass,//23.判断当前元素的如果有传进去的类名就删除，没有就增加
        }
    }
)();
```