# JS中正则
# 正则
>正则：就是用来处理复杂字符串，只能用在字符串上。
-   1.匹配字符串中的格式是否正确-->正则匹配 方法：test（返回值要么是true   要么是false）
-  2.把匹配的内容找出来-->正则的捕获 方法：exec（返回值是个数组）
```
var reg=/huini/g;

```
正则由下面的两部分组成：
>1.写在//里面的部分都是元字符（必须写）
2.写在//后面的，叫修饰符（可以不写），修饰符只有三种：g(全局匹配),i（忽略大小写），m（换行匹配）
 
#### 具有特殊意义的元字符
》**注意：** . 是除了/n以外的任意字符
>一个元字符只能匹配一个字符
>在字符串中表示一个换行就是\n。
```
var str="abc\n efd";
```
>在字符串中打几个空格就代表几个空格
>1./ \/    代表的是转义符  意思：把具有特殊意义的字符转为本来的意思
>2./\d/  匹配一个数字字符。在0-9之间
```
var s1="1d";
var reg=/\d/;
var reg1=/\\d/意思是把/d转义，匹配上面是\d的字符
console.log(reg.test(s1))
输出：true
```
>3./^/ 以什么什么开头
```
var reg=/^1/;//匹配以1开头的字符串
console.log(reg.test("12abc"));//true
console.log(reg.test("21abc"));//false
```
>4./$/ 以什么什么结尾
```
var reg=/78$/;//匹配以78结尾的字符串
console.log（reg.test("787878")）;//true

//如果是像下面一样规定了开头和结尾，中间内容就定死了，内容必须和第一行的一样
var reg=/^6abc$/;
console.log(reg.test("6abcd7"))//false

var reg=/^\d$/;//规定了开头和结尾，匹配0-9之间一个数字
console.log(reg.test("2"));//true
console.log(reg.test("22"));//false
```
|符号|意思|
|--|--|
|/\D/|匹配\d以外的任意一个|
|/\w/|匹配 0-9， a-z, A-Z, _  一共63个。这63个中的任意一个|
|/\W/ |匹配除了\w 以外任意一个|
|/\n/ |匹配一个换行符console.log("1\n2");//字符串中\n就是换行|
|/\s/| 匹配空白符（常用他来表示空格，制表符，换页符）|
|/\S/  |匹配一个非空白符|
|||
>5./\b/ 匹配一个边界。\b不能出现在；两个字符中间
```
console.log(/b\ba/.test("ba"));//false
console.log(/\ba/.test("ab"));//true
console.log(/\ba/.test("ba"));//false
console.log(/\ba\b/.test("a b a"));//true
console.log(/\ba/.test("bb  a"));//true
```
>6./\B/ 匹配一个非边界
```
console.log(/\Bb/.test("ba"));//false
console.log(/\Bb/.test("bb"));//true(只要有一个满足就可以，后面那个就满足)
console.log(/\Bb/.test("abb"));//true
```

### 正则量词元字符
>量词元字符一定要写在元字符的后面
> * 表示前面的元字符出现0次到多次
```
var reg=/\d\.*/;
console.log(reg.test("12"));//true
console.log(reg.test("12.1"));//true
console.log(reg.test("12..."));//true
console.log(reg.test("12.1.1.1"));//true
console.log(/^\d\.*/.test("12"));//true
console.log(/^\d\.*/.test("12.1"));//true
console.log(/^\d\.*$/.test("12..."));//false
console.log(/^\.\d*/.test("12.1.1.1"));//false
```

> + 前面的元字符出现1到多次
```
var reg=/^.+\d/;
console.log(reg.test("12"));//true
console.log(reg.test(".1+2"));//true
console.log(reg.test("++"));//false
console.log(reg.test("2"));//false
console.log(reg.test("pp1"));//true
console.log(reg.test("p\n1"));//false
```

> ? 前面的元字符出现0或1次
```
var reg=/^\d+\.?/;
console.log(reg.test(".2"))//false
console.log(reg.test("12.2"))//true
console.log(reg.test("0.2a"))//true
console.log(reg.test("12a"))//true
console.log(reg.test("a1.2"))//false
console.log(reg.test("1.1.1"))//true

var reg=/^\d?\.\d?$/;
console.log(reg.test("11.11"))//false
console.log(reg.test("1.1"))//true
console.log(reg.test(".11"))//false
console.log(reg.test("11"))//false
console.log(reg.test("."))//false
console.log(reg.test(".a"))//false
```

#### 元字符具体出现的次数.
 >{n}前面的元字符就出现n次
```
var reg=/^\d{3}$/;//只有三个数字
```
>{n , }前面的元字符就出现n到多次

>{n , m}前面的元字符就出现n到m次


###  | 和 []的问题
>在没有小括号的情况下，| 最后运算
>在[]中除了“|”，“-”,"^",这几个特殊符号，都只是代表本身的意思，但是转义字符“\”仍然是转义。
>x | y 表示：x或y中的一个（|可以写多个）
```
var reg=/^(0|1)$/;只匹配“1” “0”
console.log(reg.test("00"));//false
console.log(reg.test("11"));//false
console.log(reg.test("01"));//false
console.log(reg.test("0"));//true
```
>[xy] x,y中选一个，[xyzmn],xyzmn五个中选一个
```
var reg=/^[/d.]$/;//字符串的length=1
只能匹配/d或者.中的其中一个
```

>[^xy] 只要不是x,y就可以

>[a-z] 表示a-z中的一个

>[a-zA-Z] 表示a-z加上A-Z中的一个

>[] 中除了咱们说的有特殊意义的字符（^ - \ ）其他的在[]里面都是普通元字符的意义。例如：[ . ]就是表示点。
```
console.log(/^[2*]/.test("2"))//true
```
>** 注意：** 如果没有小括号的情况下，最后看|

#### 比较[xy]和x | yde 区别
```
var reg=/^10|89$/;//以10开头或者以89结尾
var reg=/^[10|89]/;//在1，0，|，8，9中选一个
var reg=/^[1089]$/；//在1，0，8，9中任选一个
var reg=/^[10-89]$/；//在1，0-8，9中选一个
var reg=/^[17-59]$/；//报错

```
>**  在正则中小括号表示分组**
>作用：1.改变优先级 先计算括号里面的
             2.表示一个小分组 \ Number 表示number个分组匹配的内容
    var reg=/^(\w)(\w{2})\2$/;
    console.log(reg.test("abcbc"));

### 正则的构造函数创建方式
>** 注意：**用构造函数创建因为是写在字符串里面，所以遇到\变成\\。
>好处：可以实现变量的拼接
```
var reg=new RegExp("^\\w\\d{4}$")
```	
    
### 匹配实例
```
匹配姓名：
  var reg=/^[\u4e00-\u9fa5]{2,4}$/
```

## 正则的捕获 exec
>分两个阶段：
-   匹配，判断字符串是否匹配正则，不匹配返回null
-  捕获，把匹配的内容捕获出来，返回一个数组。[这个数组第一项是捕获的内容，index：捕获的内容在字符串中的索引，input：原字符串]
```
var str="abcdefg";
var reg=/\d/;
console.log(reg.exec(str));//null
```
### 分组捕获
>exec返回值仍然是一个数组
-  第一项：大正则捕获的内容
-  第二项：第一个分组捕获的内容
-  第三项：第二个分组捕获的内容
-  。。。
-  index：第一项中大正则捕获内容首字符的索引
-  input：原字符串

```
var str="html5css3es6";
var reg=/([a-z]+)(\d)/g;
console.log(reg.exec(str));
console.log(reg.exec(str));
console.log(reg.exec(str));
输出：
["html5", "html", "5", index: 0, input: "html5css3es6"]
["css3", "css", "3", index: 5, input: "html5css3es6"]
["es6", "es", "6", index: 9, input: "html5css3es6"]
```
>将捕获到的放到字符串或者对象内
```
var str="html5css3es6";
var reg=/([a-z]+)(\d)/g;
var s="";
var obj={};
var re=reg.exec(str);
while (re){
    obj[re[1]]=re[2];
    s+=re[1]+"版本是"+re[2];
    re=reg.exec(str);
}
console.log(s);//输出：html版本是5css版本是3es版本是6
console.log(obj);输出：Object {html: "5", css: "3", es: "6"}

```
#### 总结：如果想要获取分组的内容只能用exec，有分组的时候exec好用，没有分组match好用

 

#### 正则的懒惰型：捕获的时候只捕获第一次匹配的内容，正则中有一个属性叫lastIndex表示的是开始查找的索引
```
var str="a1b2c1defg";
var reg=/\d/;
console.log(reg.exec(str));//["1" index:1 input:"a1b2c1defg"]
console.log(reg.exec(str));//["1" index:1 input:"a1b2c1defg"]
console.log(reg.exec(str));//["1" index:1 input:"a1b2c1defg"]
每次输出的结果是一样的，因为懒惰型
```
>解决正则懒惰型的方法：加上修饰符g
```
var str="a1b2c1defg";
var reg=/\d/g;
console.log(reg.exec(str));//["1" index:1 input:"a1b2c1defg"]
console.log(reg.exec(str));//["2" index:3 input:"a1b2c1defg"]
console.log(reg.exec(str));//["1" index:5 input:"a1b2c1defg"]
```
#### 正则的贪婪性
>贪婪性：虽然只捕获一次，但是把这次满足条件的全部捕获出来了。也就是这个整体
```
var reg=/\d+/g;
var str="womenshi2017年第qidoukao100fenyemeiyong";
console.log(reg.exec(str));
输出：
["2017", index: 8, input: "womenshi2017年第qidoukao100fenyemeiyong"]
```
>如何解决贪婪性：在量词元字符后面加上问号（？），就会捕获最短的内容
```
var reg=/\d+?/g;
var str="womenshi2017年第qidoukao100fenyemeiyong";
console.log(reg.exec(str));
输出：
["2", index: 8, input: "womenshi2017年第qidoukao100fenyemeiyong"]
```
### 只匹配不捕获
>（？：）：加在小括号里面前面表示只匹配不捕获
### match
>match 它是字符串的方法  str . match（正则表达式）
>**注意：**
-   用match的时候，正则表达式必须要加上修饰符g，否则就跟exec的结果一样。有分组的时候。
-  正则加上g捕获不到分组的内容。
-  不加修饰符g，跟exec结果一样，只能捕获一次。
>match 返回是一个数组，但是没有index和input这两个属性
```
var str="es6css3h5";
var reg=/\d/g;
console.log(str.match(reg));
返回：['6','3','5']
```

## 字符串在正则中的几个重要方法

>search()返回值是首字符的索引，没有返回-1
```
var reg=/\*\d+/;
    var str="zhufeng*2017peixunhtml5";
console.log(str.search(reg));
输出：索引7
```
>split(正则) 按照正则匹配的字符进行拆分为数组
```

```
>replace(),使用正则加上修饰符g,就可以全部替换完
```
var s="s1 s2  a1 v1";
var reg=/\s+/g;
s=s.replace(reg,"");
console.log(s);
输出：s1s2a1v1

var reg=/^\s+|\s+$/;
会把开头和结尾的空格去掉
```
>replace(正则，function（）{}).
>在中括号中如果向让-表示本身的意思，就写在最好，只要是-后面没有东西，就表示本身的意思。
replace()中的第二个参数可以传一个函数，替换一次执行一次，每一次执行都会默认给他传参数
-  第一个参数arguments[0]:大正则匹配的内容
-  第二个参数arguments[1]:第一个分组匹配的内容
-  第三个参数arguments[1]:第二个分组匹配的内容
-  。。。。
-  倒数第二个参数：就相当于exec返回值中的那个index，就是大正则匹配的内容首字符出现的索引
-  最后一个参数：就相当于exec返回值中的那个input，就是原字符串
>return什么就替换什么
```

```
### RegExp.$n：表示正则第n个分组捕获的内容
```
 var str="a1b2c3";
 var reg=/[a-z]+(\d+)[a-z]+(\d+)[a-z]+(\d+)/g;
 reg.exec(str);
 console.log(RegExp.$1);
 输出：1
$1代表的是第一个分组
在字符串中可以直接写 $1, $2，
```
、

