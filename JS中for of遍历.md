# JS中for of遍历
>只能遍历数组,不能遍历对象
```
 var ary=[1,2,3,4];
    for(let val of ary){
        //val是每一项的值
        console.log(val);//1,2,3,4
    }
```