#**["1", "2", "3"].map(parseInt)**

## parseInt() 函数

parseInt(string, radix)

string: 必需，要被解析的字符串

radix: 可选,表示要解析的数字的基数。该值介于 2 ~ 36 之间，
如果该参数小于 2 或者大于 36，则 'parseInt()' 将返回 'NaN'

如果想让 parseInt(string,radix) 返回 NaN，有两种情况：

1. 第一个参数不能转换成数字
2. 第二个参数不在 2 到 36 之间

```javascript
parseInt("10");         // 返回 10 (默认十进制)
parseInt("19",10);      // 返回 19 (十进制: 10+9)
parseInt("11",2);       // 返回 3 (二进制: 2+1)
parseInt("17",8);       // 返回 15 (八进制: 8+7)
parseInt("1f",16);      // 返回 31 (十六进制: 16+15)
parseInt("010");        // 未定：返回 10 或 8
parseInt("2","1");      // 返回 NaN
parseInt("2","0");      // 返回 2
```
