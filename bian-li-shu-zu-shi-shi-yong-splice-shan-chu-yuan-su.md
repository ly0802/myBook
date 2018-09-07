# 遍历数组时使用splice删除元素

splice\(\) 方法从数组中删除项目，然后返回被删除的项目。该方法会改变原始数组

由于splice会改变原数组，在数组循环中使用splice时需要特别注意

```js
var arr = new Array(1, 2, 3, 4, 5);     //初始化数字集合
var delete_number = 3;    //要被删除的数字

//遍历数组
for(var i=0; i<arr.length; i++){
    if(arr[i] === delete_number){   //如果找到要被删除的数字所在的数组下标
        var num = arr.splice( i, 1 );   //从i位置开始删除1个数字
        console.log("成功删除 "+num);    //输出被删除的数字
    }
    else{
        console.log(arr[i]+" 未被删除");    //如果i下标的数组元素不是需要被删除的数字，就输出数字
    }
}

// 输出：
1 未被删除
2 未被删除
成功删除 3
5 未被删除
```

输出结果少了个 4未被删除，原因就是splice改变了数组 arr，导致在删除 3 后，后面的元素往前移动一个位置，而遍历时的下标 i还是在递增加1的。所以可以在删除 3 时，下标不进行加 1，修改如下：

```js
var arr = new Array(1, 2, 3, 4, 5);     //初始化数字集合
var delete_number = 3;    //要被删除的数字

//遍历数组
for(var i=0; i<arr.length; i++){
    if(arr[i] === delete_number){   //如果找到要被删除的数字所在的数组下标
        var num = arr.splice( i, 1 );   //从i位置开始删除1个数字
        i = i - 1;
        console.log("成功删除 "+num);    //输出被删除的数字
    }
    else{
        console.log(arr[i]+" 未被删除");    //如果i下标的数组元素不是需要被删除的数字，就输出数字
    }
}

// 输出：
1 未被删除
2 未被删除
成功删除 3
4 未被删除
5 未被删除
```

也可以只有在没有删除元素时才对索引 i++， 代码修改如下：

```js
var arr = new Array(1, 2, 3, 4, 5);     //初始化数字集合
var delete_number = 3;    //要被删除的数字

//遍历数组
for(var i=0; i<arr.length; ){
    if(arr[i] === delete_number){   
        var num = arr.splice( i, 1 );   
        console.log("成功删除 "+num);    
    }
    else{
        console.log(arr[i]+" 未被删除");   
        i++；      //只有在没有删除元素时才对索引 i++
    }
}

// 输出：
1 未被删除
2 未被删除
成功删除 3
4 未被删除
5 未被删除
```

也可以使用filter这种取巧的方式，不需要再原数组上删除元素

```js
var arr = new Array(1, 2, 3, 4, 5);     //初始化数字集合
var delete_number = 3;    //要被删除的数字

arr = arr.filter(function(item){ return item !== delete_number});
// [1, 2, 4, 5]
```

#### 参考文章

* [JS的splice\(\)方法在for循环中使用可能会遇到的坑](https://blog.csdn.net/a727911438/article/details/55224532)

* [JavaScript使用for循环和splice删除数组指定元素的注意点](https://majing.io/posts/10000006121204)



