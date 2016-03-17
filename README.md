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
