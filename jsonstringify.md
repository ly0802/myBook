使用JSON.stringify将对象或数组转换字符串有些注意点

undefined、任意的函数以及 symbol 值，在序列化过程中会被忽略（出现在非数组对象的属性值中时）或者被转换成 null（出现在数组中时）

```
JSON.stringify({x: undefined, y: Object, z: Symbol("")}); 

//"{}"
```



