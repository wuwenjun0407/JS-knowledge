# JS中（扩展）括号表达式

### 1.保证一些操作语法能被浏览器识别
>第1种：自执行函数 （function（）{}）（）
>第二种：基本数据类型中的数字不可以直接调取属性和方法（因为在浏览器中，数字后面出现的第一个点表示数字的小数点）比如：1.toString 错误 应该写成1..toString或者（1）.toString
```
 console.log((1).toString());
 console.log(1..toString());
```
>第三种：引用数据类型中的对象不能直接调用方法和属性，必须通过对象名 . 属性名,或者（{}）. 属性名 例如：
```
var obj={a:1,b:2};
 console.log(obj.a);正确
 console.log({a:1,b:2}.a);错误
 console.log(({a:1,b:2}).a);正确
```
>第四种：注意再用eval遇到{}表示对象的时候用小括号包起来
```
  var s=str.split("?")[1];
    s=str.replace(/=/,":'");
    s=str.replace(/&/,"',");
    var obj=eval("({"+s+"'})");//包起来
    console.log(obj);
```
>第五种：计算的时候优先级最高
```
var s="1";
var n=2;
s=s+n+1;//"121"
s=s+(n+1);//"13"  
```
>第六种：正则中（）表示小分组，优先级最高

>第七种：本身也是有计算的效果
>一个括号中如果包含多项，它只会把最后一项的值（对于基本数据类型很任意理解，对于引用数据类型就是把他的地址值拿过来）copy过来，然后进行后续的处理
```
var a=(1,2,3,4);
 console.log(a);
 只会输出最后一项4
```
>如果最后一项是函数，那么函数执行的时候里面的this是window（就算函数前面有点也不管）
>**注意：**如果括号中只有一项，和不加括号没有区别

```
function f1() { console.log(this)}
function f2() {
    console.log(this)
}
var obj={f1:f1,f2:f2};
 (f1,f2)();//f2执行
 (f1,f2,obj.f1)()  //obj.fi的this也是window
 (obj.f1)()//obj.f1的this也是Object
```
