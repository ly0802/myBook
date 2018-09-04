在做快游戏时，碰到了一个 instanceof 类型判断的问题

## 问题描述

#### 快游戏引擎代码

canvas 的实现类 Canvas.js

```js
class Canvas {
  // 调用c++注册的api
}
```

引擎对外暴露的创建 canvas 的 api 是 qg.createCanvas\(\)

```js
qg.createCanvas = function() {
    return new Canvas()
}
```

#### h5适配层代码

适配层的 HTMLCanvasElement 实现

```js
window.HTMLCanvasElement = function() {
    return qg.createCanvas()
}
```

#### cp游戏代码

在 cp 代码里有一段 canvas 的类型判断

```js
const canvas = new window.HTMLCanvasElement()

canvas instanceof window.HTMLCanvasElement
```

希望`canvas instanceof window.HTMLCanvasElement`输出 true，但是输出了 false，为什么？

## 原因分析

[instanceof](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/instanceof) 是如何进行类型判断的？

```js
object instanceof constructor
```

instanceof 运算符用来检测 constructor.prototype 是否存在于参数 object 的原型链上。

我们来看下 cp 创建的 `canvas` 对象的原型链：

```
canvas ---> Canvas.prototype ---> Object.prototype ---> null
```

`canvas` 对象的原型链上并没有 `window.HTMLCanvasElement.prototype`，所以输出 false。

## 解决方案

如果 window.HTMLCanvasElement 

```

```



