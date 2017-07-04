# JS中字符串

## 字符串转为表达式

>**eval**将字符串转化为真正的代码，（只转换字符串）遇到大括号想表示对象的话，就用小括号抱起来，要不浏览器就会不认识，把他当做一个代码块。
```
console.log(eval("1+2+3"));
控制台输出的是括号里的和。

<script type="text/javascript">
    var str='{name:123,age:456}';
    console.log(eval(str))
</script>
会报冒号的错误。
<script type="text/javascript">
    var str='{name:123,age:456}';
    console.log(eval('({name:123,age:456}）'))
</script>
这样是正确的。

var str="{name:'123'}"
console.log(eval('({name:'123'}))
向控制台输出object{name:"123"}

```
### 如果两个字符串减法运算会默认转为数字
## 字符串

>String 对象用于处理已有的字符块（空格，换行也是字符）
>字符串是有长度的
>字符串也是对象，也有属性名和属性值，他的属性名是当前字符的索引，索引从0开始，到length结束。


#### 获取指定位置的字符（charAt索引）
>返回值：当前索引对应的字符
```
var str="abcd";
var val=str.charAt(0);//"a"
val用来接受返回值
```

#### 字符串截取

>  
  -  substr(n,m) 从索引n开始，截取m个字符
  截取后原字符串不受影响。
```
var str="abcde"
var val=str.substr(2,3);
获取到的是"cde"
``` 
>
 -  substring(n,m)从索引n开始截取到索引m处，不包含m。原数组不变
```
var str="abcde"
var val=str.substring(2,3);
获取到的是"c"
```


>  -   slice(n,m) 从索引n开始截取到索引m，不包含m，但是此方法支持参数是负数
>  支持负数作为索引（str.length+负数索引）
```
var str="abcde"
var val=str.slice(2,3);
获取到的是"c"

var str="abcde"
var val=str.slice(-2,-1);
获取到的是“d”
```

#### 查找指定字符所在字符串的索引值
> -  indexOf("指定的字符")-->返回值是该字符第一次出现位置的索引。
> -  lastIndexOf("指定的字符")  -->返回值是该字符最后一次出现位置的索引值
> -   如果没有找到，说明该字符串没有这个字符。返回-1.


#### 字符串转大写（只能转字母）
```
对象.toUpperCase()
```

#### 字符串转小写
```
对象.toLowerCase()
```

#### 替换字符
>replace(旧的字符，新的字符)替换
**注意：**不会改变员字符串，返回一个新的字符串。如果有相同字符，只能进行一次替换，就是第一个遇到的字符。

#### 查找字符串
> search（”指定的字符“）-->返回值是该字符第一次出现位置的索引。
   -   如果没有找到，说明该字符串没有这个字符。返回-1.
 
> match("指定的字符")-->["指定的字符"，index：索引，input：”123“（要查找的字符串）] 找不到返回null。
#### 字符串按照指定分隔符分成数组
>对象.split（“”）
>分隔符不会出现在数组中
```
var time="12 23 55 65";
var a=time.split(" ");
console.log(a)
输出['12,23,55,65']
```
>不加分隔符
```
var time="12 23 55 65";
var a=time.split("");
console.log(a)
输出['1','2','2','3','5','5','6','5']
```
>分隔符不存在字符串中的时候，会将字符串当做数组中的一项
```
var str="abcd";
var a=time.split("1")
console.log(a)
输出["abcd"]
```

