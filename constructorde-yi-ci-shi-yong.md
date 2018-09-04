在做快游戏时，碰到了一个 instanceof 类型判断的问题

## 问题描述

#### 快游戏引擎代码

canvas的实现类HTMLCanvasElement.js

```
class HTMLCanvasElement {
  // xxx
}
```

引擎对外暴露的创建canvas的api是qg.createCanvas\(\)

```
qg.createCanvas = function() {
    return new HTMLCanvasElement()
}
```

#### h5适配层代码

适配层的HTMLCanvasElement实现

```
window.HTMLCanvasElement = function() {
    return qg.createCanvas()
}
```

#### cp游戏代码

在cp代码里有一段canvas的类型判断

```
const canvas = new window.HTMLCanvasElement()

if (canvas instanceof window.HTMLCanvasElement) {
    console.log(true)
}
else {
    console.log(true)
}
```



