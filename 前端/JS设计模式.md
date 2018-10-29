### JS设计模式

##### 工厂模式

- 凡是用到`new`的时候, 就要考虑使用工厂模式
- 让创建对象有一个统一的入口

```typescript
class Product{
    constructor(name){
        this.name = name;
    }
    init(){
        alert("init")
    }
    fun1(){
        alert("fun1")
    }
    fun2() {
        alert("fun2")
    }
}

class Creator{
    create(name){
        return new Product(name)
    }
}

let creator = new Creator()
let p = creator.create("p1")
p.init()
p.fun1()

```

##### 单例模式

- 创建单例模式的步骤
- 1

```javascript
class SingleObject {
    login() {
        console.log("login...")
    }
}
SingleObject.getInstance = function () {
    let instance
    if (!instance) {
        instance = new SingleObject()
    }
    return instance
}

let obj1 = SingleObject.getInstance()
obj1.login()
let obj2 = SingleObject.getInstance()
console.log(obj1 === obj2)  //false

问题:
	每次instance变量在getInstance()函数执行完之后会被销毁,所以每次创建的对象都是一个新对象

考虑:
	使用闭包让变量在执行完之后不销毁
```

- 2

```
SingleObject.getInstance = function () {
    let instance
    function a(){
        if (!instance) {
            instance = new SingleObject()
        }
    }
    a()
    return instance
}

问题:
	这其实并不是一个闭包, 相当于一个函数调用, 执行完了之后变量依旧会被销毁,函数的作用域链也被销毁
	
考虑:
	真正闭包的实现方式
```

- 3

```javascript
SingleObject.getInstance = function () {
    let instance
    return function(){
        if (!instance) {
            instance = new SingleObject()
        }
    }
    return instance
}


let obj1 = SingleObject.getInstance()()
obj1.login()
let obj2 = SingleObject.getInstance()()
console.log(obj1 === obj2)  //false

问题:
	成功创建闭包, 但是结果还是false
原因:
	每次调用getInstance()方法的时候回重新声明变量instance, 相当于将保存的对象给刷掉了,从而导致匿名函数的if语句一直为真

考虑:
	在声明函数的时候就将变量声明一次, 在后续的调用当中不对instance进行声明
```

- 4

```javascript
class SingleObject {
    login() {
        console.log("login...")
    }
}
SingleObject.getInstance = (function () {
    let instance
    return function () {
        if (!instance) {
            instance = new SingleObject()
        }
        return instance
    }
})()
let obj1 = SingleObject.getInstance()
obj1.login()
let obj2 = SingleObject.getInstance()
console.log(obj1 === obj2)  //true

问题:
	当有人不知道我们的约束,直接使用obj = new SingleObject()创建对象时, 会导致单例模式失去意义

考虑:
	
```

##### 适配器模式

##### 装饰器模式

- 为对象添加新功能
- 不改变其原有的结构和功能

```javascript
class Circle{
    draw() {
        console.log("画一个圆形")
    }
}

class Decorator{
    
    constructor(circle){
        this.circle = circle
    }
    draw() {
        this.circle.draw()
        this.setRedBorder()
    }
    setRedBorder(){
        console.log("红色边框的圆")
    }
}
let circle = new Circle()
let dec = new Decorator(circle)
circle.draw()
dec.draw()


// 画一个圆形
// 画一个圆形
// 红色边框的圆
```

- 场景(未实现)

  - ES7装饰器
  - 如果node不支持,需要安装插件

  ```
  npm install babel-plugin-transform-decorators-legacy --save-dev --registry=https://registry.npm.taobao.org
  
  然后在.babelrc的plugins数组里面添加transform-decorators-legacy
  ```

































