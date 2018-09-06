使用JSON.stringify将对象或数组转换字符串有些注意点

1.undefined、任意的函数以及 symbol 值，在序列化过程中会被忽略（出现在非数组对象的属性值中时）或者被转换成 null（出现在数组中时）

```js
JSON.stringify({x: undefined, y: Object, z: Symbol("")}); 
// "{}"

JSON.stringify([undefined, Object, Symbol("")]); 
// "[null,null,null]"
```

2.对 包含循环引用的对象（对象之间相互引用，形成无限循环\) 序列话时，会抛出错误 Converting circular structure to JSON

```js
const obj1 = {}
const obj2 = {}

obj1.x = obj2
obj2.x = obj1

JSON.stringify(obj1)
// Uncaught TypeError: Converting circular structure to JSON
//   at JSON.stringify (<anonymous>)
//   at <anonymous>:1:6
```

3.不可枚举的属性会被忽略

```js
const obj = {x: 1}

Object.defineProperty(obj, 'y', {value: 2})

JSON.stringify(obj)
// "{"x":1}"
```

4.JSON.stringify\(\) 接受第二参数

