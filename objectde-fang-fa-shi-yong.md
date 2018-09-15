# Object的方法使用

---

### Object.setPrototypeOf\(obj, prototype\)

设置一个指定的对象的原型 \( 即, 内部\[\[Prototype\]\]属性）到另一个对象或 null

```js
const A = class{ print(){ } }
const dict = Object.setPrototypeOf({}, A.prototype)

dict.__proto__ === A.prototype // true
Object.getPrototypeOf(dict) === A.prototype // true
```

### Object.getPrototypeOf\(obj\)

返回指定对象的原型（内部\[\[Prototype\]\]属性的值）

```
const prototype1 = {};
const object1 = Object.create(prototype1);

Object.getPrototypeOf(object1) === prototype1 // true
```

### Object.create\(obj\)

创建一个新对象，使用现有的对象来提供新创建的对象的\_\_proto\_\_

```js
const person = {
 isHuman: false
}
const me = Object.create(person)

me.__proto__ === person // true
```



