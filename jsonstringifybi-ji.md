# JSON.stringify\(\)

`JSON.stringify()` 方法是将一个 JavaScript 值\(对象或者数组\)转换为一个 JSON 字符串。

### 语法

```
JSON.stringify(value[, replacer [, space]])
```

参数 replacer ：

| replacer | 描述 |
| :--- | :--- |
| 函数 | value的每个属性都会经过该函数的转换和处理 |
| 数组 | 只有包含在这个数组中的属性才会被序列化到最终的JSON字符串中 |
| null或未提供 | value的所有属性都会被序列化 |

```js
var replacer = function(key,value){
    if(typeof(value) == 'function'){
         return Function.prototype.toString.call(value)
    }
    return value
}
var obj = {
    bar: "new property",
    baz: 3,
    getName: function(){return 'foo'}
}

console.log(JSON.stringify(obj, replacer))
//{"bar":"new property","baz":3,"getName":"function(){return 'foo'}"}
```

关于序列化，有下面五点注意事项：

* 非数组对象的属性不能保证以特定的顺序出现在序列化后的字符串中。
* 布尔值、数字、字符串的包装对象在序列化过程中会自动转换成对应的原始值。
* `undefined、`
  任意的函数以及 symbol 值，在序列化过程中会被忽略（出现在非数组对象的属性值中时）或者被转换成
  `null`
  （出现在数组中时）。
* 对包含循环引用的对象（对象之间相互引用，形成无限循环）执行此方法，会抛出错误。
* 所有以 symbol 为属性键的属性都会被完全忽略掉，即便
  `replacer`
  参数中强制指定包含了它们。
* 不可枚举的属性会被忽略



