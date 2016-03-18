#**["1", "2", "3"].map(parseInt) 返回 [1,NaN,NaN]**

### parseInt() 函数

parseInt(string, radix)

* string: 必需，要被解析的字符串
* 如果该参数小于 2 或者大于 36，则 'parseInt()' 将返回 'NaN'

如果想让 parseInt(string,radix) 返回 NaN，有两种情况：

* 第一个参数不能转换成数字
* 第二个参数不在 2 到 36 之间

```javascript
parseInt("10");         // 返回 10 (默认十进制)
parseInt("19",10);      // 返回 19 (十进制: 10+9)
parseInt("11",2);       // 返回 3 (二进制: 2+1)
parseInt("17",8);       // 返回 15 (八进制: 8+7)
parseInt("1f",16);      // 返回 31 (十六进制: 16+15)
parseInt("010");        // 未定：返回 10 或 8
parseInt("2",1);        // 返回 NaN
parseInt("2","1");      // 返回 NaN
parseInt("2","0");      // 返回 2
```
第二个参数是0的话，0会被当做10来处理

### map 方法

对数组的每个元素调用定义的回调函数并返回包含结果的数组

array.map(callbackfn[, thisArg])

* array：必需，一个数组对象
* callbackfn：必需，一个接受最多三个参数的函数。对于数组中的每个元素，‘map’ 方法都会调用 ‘callbackfn’ 函数一次
* thisArg：可选，可在 ‘callbackfn’ 函数中为其引用 ‘this’ 关键字的对象。如果省略 ‘thisArg’，则 ‘undefined’ 将用作 ‘this’ 值

返回值
* 其中的每个元素均为关联的原始数组元素的回调函数返回值的新数组

```javascript
var numbers = [9, 16];
var result = numbers.map(Math.sqrt);

document.write(result);
// output: 3,4
```

### 重点来了
```javascript
var parseInt = function(string, radix) {
    return string + "-" + radix;
};

["1", "2", "3"].map(parseInt);

// output:
["1-0", "2-1", "3-2"]
```

map 函数将数组的值 value 传递给了 parseInt 的第一个参数，将数组的索引传递给了第二个参数。 第三个参数呢？我们再加一个参数

```javascript
var parseInt = function(string, radix, obj) {
    return string + "-" + radix + "-" + obj;
};

["1", "2", "3"].map(parseInt);

// output:
["1-0-1,2,3", "2-1-1,2,3", "3-2-1,2,3"]
```

第四个参数为 undefined，看见 map 确实为 parseInt 传递了三个参数
(element, index, array)

* 数组的值
* 数组的索引
* 数组


#**null&undefined**

### null

null 更接近「无」的意思

* 当试图获取一个不存在的对象时，那么就会返回 null
* 间接的，在函数参数中需要传入对象的位置，如果传入的不是对象，就会返回 null

### undefined

undefined 都是一种默认值的存在

* 当声明一个变量/属性后，如果没有初始化，那么默认值就是 undefined
* 如果函数没有显式注明返回值， 默认值是 undefined
* 如果函数中的参数，在调用时为获得参数，默认的也是 undefeind

### 交集
```javascript
console.log(null == undefined);    //true
```
但这也只是表明，它们在做关系运算时，都会被转换为相同的布尔值 false

### 补集
当我们使用更严格的判断方式时，两者就有了明显的差异：
```javascript
console.log(null === undefined);    //false
```

JavaScript 的数据类型分为原始值和引用值两类。因此我们也可以将「无」的划分为两部分：判定原始值是否存在的 undefined 和 判断引用值是否存在的 null

```javascript
typeof null           //"object"
typeof undefined      //"undefined"
```
### 类型转换

* 当转换为字符串时，null 和 undefiend 分别转换为字符串形式的 “null” 和 “undefiend”
* 当转换为布尔值时，null 和 undefiend 都转换布尔值 false
* 当转换为数值时，null 和 undefiend 分别转换为 0 和 NaN

### 重点来了

* undefined 是全局对象的一个属性
* 所有对象都是 Object 及其子类的实例，但 null 不是，null 更严格应该划分为原始值类型
* null 和 undefined 都可以转换为 false，但不等值于 false

#**[].reduce(Math.pow)**
### reduce()

接收一个函数作为累加器（accumulator），数组中的每个值（从左到右）开始缩减，最终为一个值

**语法:** arr.reduce(callback,[initialValue])
callback:执行数组中每个值的函数，包含四个参数

* previousValue:上一次调用回调返回的值，或者是提供的初始值（initialValue）
* currentValue 数组中当前被处理的元素
* index 当前元素在数组中的索引
* array 调用 reduce 的数组
* initialValue: 作为第一次调用 callback 的第一个参数

```javascript
[x1, x2, x3, x4].reduce(f) = f(f(f(x1, x2), x3), x4)
```

#**+运算符与三元表达式优先级**
```javascript
var val = 'smtg';
console.log('Value is ' + (val === 'smtg') ? 'Something' : 'Nothing');
```
由于+运算符优先级大于三元表达式

因此先计算 'Value is ' + (val === 'smtg') 为 'Value is true' ? 'Something' : 'Nothing'

#**+Filter**
```javascript
var ary = [0,1,2];
ary[10] = 10;
ary.filter(function(x) { return x === undefined;});
```
有没有人和我一样自信的以为是[undefined * 7]
### 重点来了
实际结果是[],因为Array.prototype.filter不会应用到缺失的元素上

#**Highest Possible Number**
```javascript
var END = Math.pow(2, 53);
var START = END - 100;
var count = 0;
for (var i = START; i <= END; i++) {
    count++;
}
console.log(count);
```

javascript仅有一种数字，它能够表示的整数范围是-2^53~2^53，所以END + 1 的值其实是等于END的，这也就造成了死循环

#**Switch**
```javascript
function showCase(value) {
    switch(value) {
    case 'A':
        console.log('Case A');
        break;
    case 'B':
        console.log('Case B');
        break;
    case undefined:
        console.log('undefined');
        break;
    default:
        console.log('Do not know!');
    }
}
showCase(new String('A'));
```
case的是使用===匹配的，而new出来的是一个Object，只有在使用==时候才等于'A'

#**Modulo Operator**
```javascript
function isOdd(num) {
    return num % 2 == 1;
}
function isEven(num) {
    return num % 2 == 0;
}
function isSane(num) {
    return isEven(num) || isOdd(num);
}
var values = [7, 4, '13', -9, Infinity];
values.map(isSane);
```
'13'会自动转换为数字13，-9%2=-1，，Infinity % 2 = NaN

#**isArray**
```javascript
Array.isArray( Array.prototype )
```
Array.prototype is an Array （[]）

#**[0]**
```javascript
var a = [0];
if ([0]) {
  console.log(a == true);
} else {
  console.log("wut");
}
```
[0]被当做true却又不等同于true
```javascript
> Boolean([0])
true
> [0] == true
false
```
#**两个空数组比较**
```javascript
console.log( [] == ![] );   //false
console.log( Boolean([]));  //true
console.log( Boolean([]) == Boolean(![]) ); //false
```
“[]”的类型“object”，而“![]”的类型是“boolean”
```javascript
console.log( [] == [] );  //false
var a = [];
console.log( a == a );    //true
```

###进行==当两个运算数的类型不同时，将它们转换成相同的类型：
* 一个数字与一个字符串，字符串转换成数字之后，进行比较。
* true转换为1、false转换为0，进行比较。
* 一个对象、数组、函数 与 一个数字或字符串，对象、数组、函数转换为原始类型的值，然后进行比较(先使用valueOf，如果不行就使用toString)

###当两个运算数类型相同，或转换成相同类型后：
* 2个字符串：同一位置上的字符相等，2个字符串就相同。
* 2个数字：2个数字相同，就相同。如果一个是NaN，或两个都是NaN，则不相同。
* 2个都是true，或者2个都是false，则相同。
* 2个引用的是同一个对象、函数、数组，则它们相等，如果引用的不是同一个对象、函数、数组，则不相同，即使这2个对象、函数、数组可以转换成完全相等的原始值。
* 2个null，或者2个都是未定义的，那么它们相等。

#**连续+-符号**
```javascript
> 1 + - + + + - + 1
2
> 1 + - + + + - - 1
0
```

1+后面的运算符全部被当做后面的1的正负号来处理

#**Arguments**
```javascript
function sidEffecting(ary) {
  ary[0] = ary[2];
}
function bar(a,b,c) {
  c = 10
  sidEffecting(arguments);
  return a + b + c;
}
bar(1,1,1)   //21
```

在javascript中变量中 arguments 是个对象，所以arguments 和局部变量所引用的内容是一样的

#**Reverse**
```javascript
var x = [].reverse;
x();
```

reverse 方法返回调用者自身,x() 的调用者是 window 对象

#**MIN_VALUE**
```javascript
Number.MIN_VALUE > 0
```
Number.MIN_VALUE 是最小的比0大的数, -Number.MAX_VALUE 可能会返回给你一个最大的负整数

#**< 隐身类型转换**
```javascript
[1 < 2 < 3, 3 < 2 < 1]   //[true, true]
```
< 会进行隐身类型转换；所以第二个表达式 3 < 2 结果为 false，false < 1 转换的结果为 true

#**== 运算符进行类型转换**
```javascript
2 == [[[2]]]        // true
```
== 运算符会进行类型转换。左右两边不断调用 toString 的结果就是 2

#**Scope**
```javascript
(function(){
  var x = y = 1;
})();
console.log(y);
console.log(x);
```
var x = y =1; 分解成实际是 var x = y; y = 1;

函数内的变量没有用 var 声明，则产生了一个隐身的全局变量

#**Regular Expression**
```javascript
var a = /123/,
    b = /123/;
a == b
a === b
```

正则表达式不能比较，因为每个正则都是唯一的

a和b都是正则实例的字面量表示，永远都不会相等

类似：var a = {a: 1},b = {a: 1}; a==b;a===b 结果是 false 一样

#**Arrays are compared lexicographically with > and <,**

```javascript
var a = [1, 2, 3],
    b = [1, 2, 3],
    c = [1, 2, 4]
a ==  b
a === b
a >   c
a <   c
```

数组通过>和<会安顺序比较, 但==和===不会

#**Trailing Comma**
```javascript
[,,,].join(", ")
```

Javascript 数组允许以 , 号结尾。所以题目中的数组实际上是一个 undefined * 3 的数组。

相当于[undefined, undefined, undefined,] => [undefined, undefined, undefined]

#**Reserved Words**
```javascript
var a = {class: "Animal", name: 'Fido'};
a.class
```

输出需要看是什么浏览器 class 是保留字, 在chrome Firefox 和 Opera中可作为属性名, 但IE不行

#**Date**

### Date()

作为一个函数，Date对象可以直接调用，返回一个当前日期和时间的字符串
可以看到无论Date括号里面输入那些格式的变量,最终都返回当前时间

```javascript
> Date()
=> "Fri Mar 18 2016 11:15:53 GMT+0800 (CST)"
> Date(1)
=> "Fri Mar 18 2016 11:16:01 GMT+0800 (CST)"
> Date(2016,3,8)
=> "Fri Mar 18 2016 11:16:11 GMT+0800 (CST)"
> Date("2016-3-8")
=> "Fri Mar 18 2016 11:16:40 GMT+0800 (CST)"
```

### new Date()

Date对象还是一个构造函数，对它使用new命令，会返回一个Date对象的实例。如果不加参数，生成的就是代表当前时间的对象*返回字符串*

* new Date(milliseconds)

Date对象接受从1970年1月1日00:00:00 UTC开始计算的毫秒数作为参数。这意味着如果将Unix时间戳作为参数，必须将Unix时间戳乘以1000

```javascript
> new Date(0)
=> Thu Jan 01 1970 08:00:00 GMT+0800 (CST)
> new Date(10000)
=> Thu Jan 01 1970 08:00:10 GMT+0800 (CST)
> new Date(3600 * 24 * 1000)
=> Fri Jan 02 1970 08:00:00 GMT+0800 (CST)
```
* new Date(datestring)

Date对象还接受一个日期字符串作为参数，返回所对应的时间*返回object*

```javascript
new Date("2013-2-15")
new Date('2013/2/15')
new Date("2013-FEB-15")
new Date("FEB, 15, 2013")
new Date("FEB 15, 2013")
new Date("Feberuary, 15, 2013")
new Date("Feberuary 15, 2013")
new Date("15, Feberuary, 2013")

// 上面多种日期字符串的写法，返回的都是同一个时间
```

* new Date(year, month [, day, hours, minutes, seconds, ms])

Date对象还可以接受多个整数作为参数，依次表示年、月、日、小时、分钟、秒和毫秒。

如果采用这种格式，最少需要提供两个参数（年和月），其他参数都是可选的，默认等于0。因为如果只使用“年”这一个参数，Date对象会将其解释为毫秒数

```javascript
new Date(2013)
// Thu Jan 01 1970 08:00:02 GMT+0800 (CST)

new Date(2013, 0)
// Tue Jan 01 2013 00:00:00 GMT+0800 (CST)

new Date(2013, 0, 1)
// Tue Jan 01 2013 00:00:00 GMT+0800 (CST)

new Date(2013, 0, 1, 0)
// Tue Jan 01 2013 00:00:00 GMT+0800 (CST)

new Date(2013, 0, 1, 0, 0, 0, 0)
// Tue Jan 01 2013 00:00:00 GMT+0800 (CST)
```

### 重点来了

```javascript
var a = new Date("epoch")
```

得到的是一个无效日期"Invalid Date"

```javascript
var a = new Date("2014-03-19"),
    b = new Date(2014, 03, 19);
[a.getDay() === b.getDay(), a.getMonth() === b.getMonth()]

// => [false, false]
```

Date构造函数可以传入多种类型的参数, 但如果是传入多个参数, 代表月份的第二个参数是从0开始的, 也就是3代表4月

#**Function.length**
```javascript
var a = Function.length,
    b = new Function().length
a === b
```

这个问题等同于问Function.length === Function.prototype.length

一个是Function自己参数的长度，一个是通过Function构造函数继承过来参数的长度

#**Match**
```javascript
if ('http://giftwrapped.com/picture.jpg'.match('.gif')) {
  'a gif file'
} else {
  'not a gif file'
}
```

匹配上的是["/gif"]

#**Math min & max**
```javascript
var min = Math.min(), max = Math.max()
min < max
```

当没有传入参数的时候Math.min()返回Infinity,Math.max()将会返回-Infinify
