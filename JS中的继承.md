# JS中的继承

>继承：子类继承父类的属性和方法
#### 原型继承
>子类(F2)的原型指向父类（F1）
>这样的话，子类（F2）的原型上就会有通过父类（F1）得来的私有属性，还可以通过F2.prototype._ _proto_ _得到F1的原型（F1.prototype）上的共有属性
>那么以后在创建F2的实例的时候，就可以一级一级往上找，找到F1的原型
```
    function F1() {
        this.x=100;
    }
    function F2() {

    }
    F1.prototype.getX=function () {
        console.log(this.x);
    };
    F2.prototype=new F1();//继承的核心


    var f2=new F1();
    //F2是F1的一个实例
    //F2.prototype.__proto__-->F1.prototype
    F2.prototype.getX();//-->this=F2.prototype
    console.log(f2.getX()===F2.prototype.getX())
```

#### call继承
>改变this
```
  function F1() {
       this.x=100;
       this.y=200;
   }
   F1.prototype.getX=function () {
       console.log(this.x)
   };
   function F2() {
       //this-->F2的实例，f2
       //F1()->this=window，
       F1.call(this);
   }
   var f2=new F2();
```
#### 冒充对象
>