### 



### Boolean()

- `Boolean()`函数可将其他类型转化为`true or false`

  ![1538098615473](C:\Users\hanzhuo\AppData\Local\Temp\1538098615473.png)

  ![1538098625233](C:\Users\hanzhuo\AppData\Local\Temp\1538098625233.png)

### Number

- 运算误差

  ![1538099103469](C:\Users\hanzhuo\AppData\Local\Temp\1538099103469.png)

- `isFinite()`

  - Number.MIN_VALUE----js能表示的最小数值
  - Number.MAX_VALUE----最大值
  - 超出js能表示的范围则被转化为`-Infinity 或者 Infinity`, 但是无法进行下一次运算
  - 用`isFinite()`确定该数值是不是无穷的![1538099412684](C:\Users\hanzhuo\AppData\Local\Temp\1538099412684.png)

- `NaN`

  ![1538099526508](C:\Users\hanzhuo\AppData\Local\Temp\1538099526508.png)

  - `isNaN`

    ![1538099610323](C:\Users\hanzhuo\AppData\Local\Temp\1538099610323.png)

- 数值转换

  - `Number()`

  - `parseInt()`

  - `parseFloat()`

    ![1538099755829](C:\Users\hanzhuo\AppData\Local\Temp\1538099755829.png)

  - `Number()`转换不合理, 使用其他两个方法
  - `parseInt()`对空字符转化为`NaN`,`Number()`会返回0

  - `parseInt`转化规则

    ![1538100120204](C:\Users\hanzhuo\AppData\Local\Temp\1538100120204.png)

  - 转换基数

    ![1538100351187](C:\Users\hanzhuo\AppData\Local\Temp\1538100351187.png)

    - 建议无论什么情况都加上基数



### String

- `toString()`

  - 不会转化`null`和`undefined`

- `String()`

  ![1538100786587](C:\Users\hanzhuo\AppData\Local\Temp\1538100786587.png)



### Object

- 创建自定义对象

  ```javascript
  var o = new Object()
  /** 可省略括号, 但不推荐 **/ 
  var o = new Object
  ```

- `Constructor`

  - 保存创建当前对象的函数, 前一个例子中即是`Object()`这个函数

- `hasOwnProperty`

  - 检查属性在对象中是否存在, 参数应传入字符串
  - `o.hasOwnProperty("name")`

- `isPrototypeOf(object)`

  - 检查传入对象是否是另外一个对象的原型



### 操作符

- 一元加操作符

  ```javascript
  var num = 25
  num = + 25 //仍然是25
  ```

  - 会像`Number`一样转换数值

    ![1538101737409](C:\Users\hanzhuo\AppData\Local\Temp\1538101737409.png)

- 一元减操作符

  - 主要用于表示负数

    ```js
    var num = 235
    num = -num  // -235
    ```

  - 转换规则

  ![1538101811376](C:\Users\hanzhuo\AppData\Local\Temp\1538101811376.png)

- 布尔操作符

  - 逻辑非

    ![1538101976466](C:\Users\hanzhuo\AppData\Local\Temp\1538101976466.png)

  - 逻辑或

    ![1538102104056](C:\Users\hanzhuo\AppData\Local\Temp\1538102104056.png)

- 乘法操作符

  - 如果其中一个操作数不是数值, 会使用`Number()`先进行转换, 空字符串为0, `true`为1

    ```js
    NaN * x = NaN
    Infinity * 0 = NaN
    Infinity * Infinity = Infinity
    ```

- 除法

  - 如果一个操作符为NaN, 结果也是NaN

  ```javascript
  Infinity / Infinity = NaN
  0 / 0 = NaN
  1 / 0 = Infinity
  200000 / 0 = Infinity
  Infinity / x = Infinity or -Infinity
  ```

  - 如果不是数值, 则会被转换



### 语句

- label语句

  - label: statement

  ```javascript
  start: for(var i = 0; i <count; i++){
      alert(i)
  }
  ```

  - 配合`break` `continue`使用

  ![1538103451879](C:\Users\hanzhuo\AppData\Local\Temp\1538103451879.png)

  - 上面图片中`outermost`就是`label`标签

    ![1538103557512](C:\Users\hanzhuo\AppData\Local\Temp\1538103557512.png)



### 变量, 作用域和内存问题

##### 引用类型

-  在操作对象时, 实际上实在操作对象的引用而不是实际的对象, 为此, 引用类型的值是按引用访问的'

- 复制对象值

  - 复制引用类型的变量时, 实际上是复制一个指针, 两个指针指向同一个对象

  ```js
  var obj1 = new Object()
  var obj2 = obj1 // 复制对象
  obj1.name = "hanzhuo"
  alert(obj2.name) // "hanzhuo"
  ```

  ![1538106723228](C:\Users\hanzhuo\AppData\Local\Temp\1538106723228.png)

##### 没有块级作用域

```js
if(true){
    var color = "blue"
}
alert(color) // blue
/**************************/
for(var i = 0; i < 10; i++){
    doSomething(i)
}
alert(i) // 10
```

- `i`即使在for循环结束后, 也会存在于循环外部的执行环境中

- `var`声明的变量会自动添加到最接近的环境中

  - 上面两个例子最接近的环境即`if`和`for`本身所在的环境
  - 在函数内部, 最接近的环境就是函数的局部环境, 即函数内部

  ```js
  function add(num1, num2){
      var sum = num1 + num2  // 如果省略var, 就会被添加到全局环境中
      return sum
  }
  var result = add(10, 20)
  alert(sum)  //会导致报错
  ```

##### 管理内存

![1538123889813](C:\Users\hanzhuo\AppData\Local\Temp\1538123889813.png)

### 引用类型

##### Object 类型

- 访问方法

  - 点表示法(推荐)
  - 方括号表示法

  ```js
  alert(person['name'])
  ```

   - 方括号法可以通过变量来访问属性

  ```js
  alert(person[propertyName])
  ```

  - 包含会导致语法错误的字符可用方括号访问

  ```js
  /** 包含空格, 不能用点表示法访问 **/
  person['first name'] = 'hanzhuo' 
  ```

##### Array 类型

- 数组大小可以动态调整 , 可以随着数据的添加自动增长以容纳新的数据

- 创建数组的方法

```javascript
var colors = new Array() // new可省略
var colors = new Array(20) // 创建20个项的数组
var colors = new Array('red', 'blue') // 两项, 每一项的值为对应参数


/** 数组字面量 **/
var colors = ['red', 'blue']
var name = [] // 空数组
var values = [1, 2,] //不可取, 会创建一个包含2或3项的数组
var options = [,,,,,] // 不可取, 会创建包含5或6项的数组
```

- 数组字面量并不会调用`Array`构造函数, 同对象一样

- 自动添加长度

```javascript
var colors = ['red', 'blue']
colors[1] = 'green' // 修改第二项
colors[2] = 'black' //新增第三项
```

- `length`不是只读的, 可修改

```javascript
var colors = ['red', 'blue']
colors.length = 1
alert(colors[1])  // undefined

/** 如果将length的值设置为大于数组项数的值, 则新增的每一项都会取得undefined值 **/
var colors = ['red', 'blue']
colors.length = 3
alert(colors[2])  // undefined

/** 利用length在数组末尾添加新项 **/ 
var colors = ['red', 'blue']
colors[colors.length] = 'green'
colors[colors.length = 'brown'
```

- 检测是否是数组

![1538126067305](C:\Users\hanzhuo\AppData\Local\Temp\1538126067305.png)

- 排序方法

  - `reverse()`
  - `sort()` 默认升序

  ```javascript
  var values = [1,2,3,4]
  values.reverse()  // 4,3,2,1
  
  var values = [0, 1, 5, 10, 15]
  values.sort() // 0, 1, 10, 15, 5
  ```

   - `sort()`方法会调用每个数组项的`toString()`方法, 然后比较得到的字符串, 所以会出现上面的排序不正常的情况

  - 因此, `sort()`方法可以接收一个比较函数作为参数

    - 第一个参数在第二个参数前面则返回一个负值
    - 在后面返回正值
    - 相等则为0

    ```javascript
    /** 升序 **/ 
    function compare(value1, value2){
        if(value1 < value2){
            return -1  // 可以表示为不需要交换位置
        }else if(value1 > value2){
            return 1  // 需要交换位置
        }else{
            return 0
        }
    }
    /** 或者 **/
    function compare(value1, value2){
        return value1 - value2   //此时为升序
    }
    
    
    /** 降序 **/
    function compare(value1, value2){
        if(value1 < value2){
            return 1  // 小于的话就交换位置
        }else if(value1 > value2){
            return -1
        }else{
            return 0
        }
    }
    ```

- 操作方法

  - `concat()`

    - 会创建当前数组的一个副本, 不会改变原数组
    - 可以传一个或多个数组
    - 如果不是数组, 则被简单添加到末尾

    ```javascript
    var colors = ['red', 'green', 'blue']
    var colors2 = colors.concat('yellow', ['black', 'brown'])
    
    alert(colors)  //red,green,blue (alert需要传递字符串, 所以会调用colors中每一项的toString()方法,然后通过逗号连接输出)
    alert(colors2) // red,green,blue,yellow,black,brown
    ```


  - `slice()`

    - 不改变原来数组
    - 只有一个参数会返回指定位置到末尾的所有项
    - 两个参数, 返回其实和结束位置但不包括结束位置的项

    ![1538128464226](C:\Users\hanzhuo\AppData\Local\Temp\1538128464226.png)

    - 如果参数中有一个负数, 则用数组长度加上该数来确定相应位置

    ```
    在一个五项中的数组上调用slice(-2, -1)与调用slice(3, 4)得到的结果相同
    ```

    - 如果结束位置小于起始位置, 则返回空数组

  - `splice()`方法





















