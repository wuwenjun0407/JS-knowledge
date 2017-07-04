# JS中Date（时间类）

## Date的应用（时间类）
>Date 对象会自动把当前日期和时间保存为其初始值
在项目中不会获取自己本机的时间，而是获取服务器的时间
将时间格式转换为标准时间格式
var tDate=new Date('2016-11-01 10:01:01')
在ie67下'-'不支持需要改成'/'
var tDate=new Date('2016/11/01 10:01:01')


>通过这个对象可以获取本机时间
>Date 对象用于处理日期和时间
```
var time=new Date();
    console.log(time)
 控制台输出：   
Thu Apr 20 2017 10:33:23 GMT+0800 (中国标准时间)
```

>var year=time.getFullYear();//设置 Date 对象中的年份（四位数字）
var month=time.getMonth();//根据世界时设置 Date 对象中的月份 (0 ~ 11) 
var day=time.getDate();//从 Date 对象返回一个月中的某一天 (1 ~ 31)
var week=time.getDay();//从 Date 对象返回一周中的某一天 (0 ~ 6) 代表周日-周六
var hours=time.getHours();//返回 Date 对象的小时 (0 ~ 23)
var minutes=time.getMinutes();//返回 Date 对象的分钟 (0 ~ 59)
var seconds=time.getSeconds();//返回 Date 对象的秒数 (0 ~ 59)
var mSeconds=time.getMilliseconds();//返回 Date 对象的毫秒(0 ~ 999)


### 格林尼治时间转北京时间
```
 let time=xhr.getResponseHeader("date");
 //获取的是格林尼治时间
  time=new Date(time);//转为北京时间
```

