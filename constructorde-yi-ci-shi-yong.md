在做快游戏时，碰到了一个 instanceof 类型判断的问题：

引擎代码：

HTMLCanvasElement.js 

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



