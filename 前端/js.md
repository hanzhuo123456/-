前端书籍推荐

- [伯乐在线](https://github.com/jobbole/awesome-web-dev-books)

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

    ```js
    在一个五项中的数组上调用slice(-2, -1)与调用slice(3, 4)得到的结果相同
    ```

    - 如果结束位置小于起始位置, 则返回空数组

  - `splice()`方法

    - 删除--删除任意数量的项, 指定2个参数:要删除第一项的位置和要删除的项数
      - `splice(0,2)`会删除数组前两项

    - 插入--提供3个参数: 起始位置, 0(要删除的项数)和要插入的项, 可以插入多个项

    ```
    splice(2, 0, 'red', 'green')
    ```

    - 替换--3个参数, 同插入, 删除的项数不为0

    ```
    splice(2, 1, 'red', 'green')
    ```

    ![1538202272552](C:\Users\hanzhuo\AppData\Local\Temp\1538202272552.png)

- 位置方法

  - `indexOf()`
    - 接收两个参数

    - 要查找的项和表示查找起点位置的索引
    - 从数组开头查找
    - 返回要查找的项在数组中的位置, 没找到返回-1
    - 内部使用的是全等操作符, 所以要求查找的项必须严格相等

  - `lastIndexOf()`
    - 同`indexof`用法一样, 不同的是它会从数组末尾开始查找

- 迭代方法

  - 三个参数--数组项的值, 该项在数组中的位置和数组本身
  - 初始数组

  ```javascript
  var numbers = [1, 2, 3, 4, 5, 4, 3, 2, 1]
  ```

  - `every()`
    - 函数对数组每一项都返回`true`, 则返回`true`

  ```javascript
  var everyResult = numbers.every(function(item, index, array){
      return (item >2)
  })
  alert(everyResult)  // false
  ```

  - `some()`
    - 和`every`差不多, 不同的是`some()`方法其中一项返回`true`, 就会返回`true`
  - `filter()`
    - 返回`true`项组成的数组

  ```
  var filterResult = numbers.filter(function(item, index, array){
      return item > 2
  })
  alert(filterResult)  // [3, 4, 5, 4, 3] 
  ```

  - `map()`
    - 返回每次函数调用的结果组成的数组

  ```
  var mapResult = numbers.map(function(item, index, array){
      return item * 2
  })
  alert(mapResult)  // [2,4,6,8,10,8,6,4,2] 
  ```

  - `forEach()`
    - 循环

  - `reduce()`

    - 从数组第一项逐个遍历数组

    - 4个参数, 前一个值, 当前值, 项的索引, 数组对象
    - 函数返回的值作为第一个参数传给下一项

  ```javascript
  var values = [1, 2, 3, 4, 5]
  var sum = values.reduce(funtion(prev, cur, index, array){
      return prev + cur
  })
  
  alert(sun) // 15
  ```

  - `reduceRight()`
    - 从最后一项开始遍历数组
    - 和`reduce()`用法相同

##### Date 类型

- 创建日期对象

```javascript
/** 不传递参数的情况, 会自动获得当前日期和时间 **/
var now = new Date()

```

- 根据特定的日子和时间创建对象, 必须传入表示该日期的毫秒数

- 为了简化计算过程, 提供了`Date.parse()`和`Data.UTC()`两个方法

- `Date.parse()`

  - 接收一个表示日期的字符串参数
  - 这个方法的行为因实现而异, 因地区而异

  - 参数支持以下几种

  ![1538211501821](C:\Users\hanzhuo\AppData\Local\Temp\1538211501821.png)

  - 传入的参数字符串不能表示日期, 会返回`NaN`
  - 直接将字符串给`Date`构造函数, 也会在后台调用`Date.parse()`

  ```
  var someDate = new Date('May 25, 2004');
  ```

  - 注意

  ![1538211658407](C:\Users\hanzhuo\AppData\Local\Temp\1538211658407.png)

- `Date.UTC()`

  - 返回表示日期的毫秒数

![1538211747128](C:\Users\hanzhuo\AppData\Local\Temp\1538211747128.png)



 - `Date`构造函数模仿`Date.UTC()`

![1538211841185](C:\Users\hanzhuo\AppData\Local\Temp\1538211841185.png)

- `Date.now()`

  - 返回表示调用这个方法时的日期和时间的毫秒数

  ```javascript
  var start = Date.now()
  
  doSomething()
  
  var stop = Date.now()
  result = stop - start
  ```

- `+`

  - 使用`+`操作符把`Date`对象转化为字符串

  ```javascript
  var start = +new Date()
  
  doSomething()
  
  var stop = +new Date()
  result = stop - start
  ```

- `getDate()`

  - 获取天数

- `getDay*()`

  - 返回星期几(0-->星期日, 6-->星期六)

##### RegExp类型

- 创建正则表达式

```javascript
var expression = /pattern/ flags;
```

 - `flags`取值

![1538212415039](C:\Users\hanzhuo\AppData\Local\Temp\1538212415039.png)

```javascript
var pattern = /.at/gi
```

- 需要转义的元字符

```
( [ { \ ^ $ | ) ? * + . ] }
```

-  在ECMA5中,使用`/pattern/`创建的和使用`RegExp`构造函数创建的实例都是一个新实例,

- `RegExp`实例属性
  - `global`
    - 布尔值, 表示是否设置了g标志
  - ignoreCase
    - 布尔值,是否设置`i`标志
  - lastIndex
    - 整数, 开始搜索下一个匹配项的字符位置, 从0算起
  - multiline
    - 布尔值, 是否设置了`m`标志
  - source
    - 正则表达式字符串

![1538213188238](C:\Users\hanzhuo\AppData\Local\Temp\1538213188238.png)

- `RegExp`实例方法

  - `exec()`

    - 接收一个参数, 即要被正则表达式查询的字符串
    - 返回第一个匹配项的数组, 在没有匹配项的情况下返回`null`
    - 包含`index`和`input`两个额外数组属性
    - index表示匹配项在字符串中的位置
    - input表示源字符串
    - 数组中, 第一项是匹配到的字符串, 其他项是捕获组匹配的字符串

    ![1538213403712](C:\Users\hanzhuo\AppData\Local\Temp\1538213403712.png)

    - 设置了全局标志也会返回第一个匹配项, 与不设置的区别在与, 当下一次调用`exec()`时, 会在字符串中继续查找新匹配项, 而不是从头开始查找
    - 一下的例子中全局有一个错误之处, 即第一次`lastIndex`为3

    ```javascript
    var text1 = 'cat, bat, vat, fat'
    var pattern1 = /.at/g
    var matches = pattern1.exec(text1)
    pattern1.lastIndex  //3,不是0
    ```



    ![1538213804384](C:\Users\hanzhuo\AppData\Local\Temp\1538213804384.png)

  - `test()`

    - 接受源字符串
    - 模式匹配到的情况下返回`true`, 否则返回`false`
    - 经常用在`if`语句中

    ```javascript
    var text = '000-00-0000'
    var pattern = /\d{3}-\d{2}-\d{4}/
    
    if(pattern.test(test)){
        alert('ok')
    }
    ```

- `RegExp`构造函数属性

  ![1538214631635](C:\Users\hanzhuo\AppData\Local\Temp\1538214631635.png)

##### Function 类型

- 函数是对象
- 函数名实际上是指向函数对象的指针

- 函数声明和函数表达式
  - 解析器会率先读取函数声明,  并使其在任何代码之前可用
  - 函数表达式, 必须等到执行到它所在的代码行

- 结合`sort()`方法根据属性名来排序

```javascript
function createComparisonFunction(propertyName){
    return function(object1, object2){
        value1 = object1[propertyName];
        value2 = object2[propertyName];
        if(value1 <value2){
            return -1;
        }else if(value1 > value2){
            return 1;
        } else {
            return 0;
        }
    }
}

var data = [{name: 'Zachary', age:28}, {name:'Nicholas', age: 29}]
data.sort(createComparisonFunction('name'))
alert(data[0].name)  // Nicholas
```

- 函数内部属性
  - `arguments`对象有一个`callee`属性,是指针, 指向拥有这个`arguments`对象的函数

```javascript
function factorial(num){
    if (num <= 1){
        return 1;
    } else {
        return num * factorial(num-1)
    }
}

/** 以上阶乘函数存在一个问题, 函数的执行与函数名factorial紧紧耦合在一起, 为了松耦合, 可以向下面这样使用 **/

function factorial(num){
    if (num <= 1){
        return 1;
    } else {
        return num * arguments.callee(num-1)
    }
}
/** 严格模式下arguments.callee会导致错误 **/
```

- 函数的`length`属性
  - `length`的值为参数的个数

```javascript
function sayName(name){
    alert(name)
}
function sun(sum1, sum2){
    return num1 + num2
}
function sayHi(){
    alert('hi')
}

alert(sayName.length)  // 1
alert(sum.length)    //2
alert(sayHi.length)  // 0
```

- `apply()`

  - 接收两个参数: 一个是在其中运行函数的作用域, 另一个是参数数组
  - 第二个参数可以是`Array`的实例, 也可以是`arguments`对象

  ![1538963352376](C:\Users\hanzhuo\AppData\Local\Temp\1538963352376.png)

  - 上图中的`this`会被转化为`window`对象, 但是在严格模式中, 并不会转化, `this`将是`undefined`

- `call()`

  - 和`apply()`方法相同, 区别在于给函数的参数必须一一列举出来

  ![1538963597645](C:\Users\hanzhuo\AppData\Local\Temp\1538963597645.png)

- `bind()`

  ![1538963845346](C:\Users\hanzhuo\AppData\Local\Temp\1538963845346.png)

  ### 基本包装类型

  ------



  - 基本包装类型的对象, 实例之存在于一行代码的执行瞬间, 然后立即被销毁

  - `Number` `String` `Boolean`

  ```javascript
  var s1 = 'some text';
  s1.color = 'red';
  alert(s1.color); // undefined
  ```

  - `Number`
    - `toFiexed()`
      - 返回字符串

  ```javascript
  var num = 10.005
  alert(num.toFixed(2)) // "10.01" 
  ```

   - `toExponential()`
     - 返回指数表示法（字符串）

  ```javascript
  var num = 10
  alert(num.toExponential(1))  // "1.0e+1"
  ```

   - `toPrecision()`

     -  可能会返回`fixed`格式,也可能返回指数格式

  ```javascript
  var num = 99
  alert(num.toPrecision(1)) // 1e+2
  alert(num.toPrecision(2)) // 99
  alert(num.toPrecision(3)) // 99.0
  ```

- `String`

  - 具有`length`属性

  - 字符方法

    - `charAt()`和`charCodeAt()`

    ```javascript
    var stringValue = 'hello world';
    stringValue.charAt(1) // 'e'
    
    stringValue.charCodeAt(1) // '101', 小写字母e的字符编码
    ```

    - 方括号访问字符

    ```javascript
    stringValue[1]; //'e'
    ```

  - 字符串操作方法

    - `concat()`

    ```javascript
    var stringValue = 'hello ';
    var result = stringValue.concat('world');
    alert(result)  // 'hello world'
    alert(stringValue)  // 'hello'
    
    result = stringValue.concat('world', '!');
    alert(result) // 'hello worldworld!
    alert(stringValue) // 'hello'
    ```

    - 使用的更多是`+`拼接字符串
    - `slice()`, `substr()`, `substring()`
      - 都不影响原字符串

    ![1538968806736](C:\Users\hanzhuo\AppData\Local\Temp\1538968806736.png)

     - 其中`substr()`第二个参数表示要返回的字符个数

     - 当传入的参数是负值的情况下

       - `slice()`会将传入的负值与字符串的长度相加
       - `substr()`会将符的第一个参数加上字符串的长度, 将负的第二个参数转换为0
       - `substring()`将所有负值都转换为0

       ![1538969040748](C:\Users\hanzhuo\AppData\Local\Temp\1538969040748.png)

    - `trim()`

      - 创建副本, 删除前置和后缀空格, 原始字符串不变

    - `fromCharCode()`

      - 静态方法
      - 接收一或多个字符编码, 转化成 一个字符串

      ```
      alert(String.fromCharCode(104, 101)); // he
      ```


- 单体内置对象

  - `Global`对象

    - 方法
      - `isNaN()`
      - `isFinite()`
      - `parseInt()`
      - `parseFloat()`

    - `URI`编码方法

      - 对URI进行编码, 用特殊的`UTF-8`编码替换所有无效的字符, 让浏览器能够接受和理解
      - `encodeURI()`
        - 主要用于整个`URI`, 如`http://www.wrox.com/illegal value.htm`
        - 不会对属于`URI`的特殊字符进行编码, 例如冒号, 正斜杠, 问号和井字号
      - `encodeURIComponent()`
        - 对`URI`	中的某一段(如前面的`illegal value.htm`进行编码
        - 对它发现的任何非标准字符进行编码

      ```
      var uri = 'http://www.wrox.com/illegal value.htm#start';
      alert(encodeURI(uri)) // 'http://ww.wrox.com/illegal%20 value.htm#start'
      
      alsert(encodeURIComponent(uri)) // "http%3A%2F%2Fwww.wrox.com%2Fillegal%20value.htm%23start"
      ```

      - 在实际中使用`encodeURIComponent()`方法更多, 实践中更常见的只是对查询字符串参数编码

      - 解码函数对应的是`decodeURI()`和`decodeURIComponent()`

    - `eval()`方法

      - 只接受一个参数, `javascript`字符串
      - 可以引用在包含环境中定义的变量

      ```
      var msg = 'hello world';
      eval('alert(msg)'); //'hello world' 
      ```

      - 可以定义一个函数, 并在外部调用

      ```
      eval("function sayHi(){alert('hi');}")
      sayHi()
      ```

      - 定义变量同理



### 面向对象的编程方法

------

##### 数据属性

- `[[ Configurable ]]`

  - 能否通过`delete`删除属性从而重新定义属性
  - 默认为`true`

- `[[Enumerable]]`

  - 能否通过`for-in`循环返回属性
  - 默认为true

- `[[Writable]]`

  - 能否修改属性的值
  - 默认为true

- `[[Value]]`

  - 包含这个属性的数据值
  - 读取属性值时从这个位置读,写入属性值时把新值保存在这个位置
  - 默认为`undefined`

  ```
  var person = {
      name:'Nicholas'
  }
  
  // [[Value]]特性被设置为'Nicholas', 对这个值的任何修改都将反映在这个位置
  ```

- `Object.defineProperty()`

  - 修改属性默认的特性
  - 接收三个参数, 属性所在的对象, 属性的名字和一个描述符对象
  - 描述符对象属性必须是
    - `configurable`
    - `enumerable`
    - `writable`
    - `value`
  - 设置一个或多个值, 可以修改对应的特性值

  ```javascript
  var person = {};
  Object.defineProperty(person, 'name',{
      writable: false, // 不可修改
      value: 'Nicholas',
      configurable: false //不可删除
  })
  
  alert(person.name) // 'Nicholas'
  person.name = 'Greg';  // 严格模式下会抛出错误
  alert(person.name); //'Nicholas'
  
  delete person.name; // 严格模式下会抛出错误
  ```

  - 一旦把属性设置为不可配置(`configurable: false`)后, 就不能变回可配置的了。此时， 再调用`Object.defineProperty`方法修改除`writable`之外的特性, 都会导致错误

  ```javascript
  var person = {};
  Object.defineProperty(person, 'name',{
      value: 'Nicholas',
      configurable: false //不可删除
  })
  
  //抛出错误
  Object.defineProperty(person, 'name',{
      value: 'Nicholas',
      configurable: true //不可删除
  })
  ```

  - 不建议在ie8中使用这个方法

##### 访问器属性

- `[[ Configurable ]]`
  - 能否通过`delete`删除属性从而重新定义属性
  - 默认为`true`
- `[[Enumerable]]`
  - 能否通过`for-in`循环返回属性
  - 默认为true
- `[[Get]]`
  - 读取属性时调用的函数
  - 默认为`undefined`
- `[[Set]]`
  - 写入属性时调用的函数
  - 默认为`undefined`
- 访问器属性不能直接定义, 必须使用`Object.defineProperty()`来定义

```javascript
var book = {
    _year: 2004,
    edition: 1
};

Object.defineProperty(book, 'year', {
    get: function(){
        return this._year;
    },
    set: function(newValue){
        if(newValue > 2004){
            this._year = newValue;
            this.edition += newValue -2004;
        }
    }
});

book.year = 2005;
alert(book.edition); // 2
```

- 只指定`getter`意味着属性不能写,

- 定义多个属性

  - `Object.defineProperties()`

    - 接收两个对象参数
    - 第一个对象是要添加和修改其属性的对象,
    - 第二个对象的属性和第一个对象中要添加或修改的属性一一对应.

    ```javascript
    var book = {};
    Object.defineProperties(book, {
        _year: {
            value:2004
        },
        edition: {
            value: 1
        },
        year:{
            get: function() {
                return this._year;
            },
            set: function(newValue){
            if(newValue > 2004){
                this._year = newValue;
                this.edition += newValue -2004;
            }
      	 }
        }
    })
    
    var descriptor = Object.getOwnPropertyDescriptor(book, '_year');
    alert(descriptor.value); // 2004
    alert(descriptor.configurable)   // false
    ```


##### 工厂模式

```javascript
function createPerson(name, age, job){
    var o = new Object();
    o.name = name;
    o.age = age;
    o.job = job;
    o.sayName = function() {
        alert(this.name)
    };
    return o;
}
var person1 = createPerson('hanzhuo', 29, 'softwate Engineer')
var person2 = createPerson('greg', 29, 'softwate Engineer')
```

- 优点
  - 解决相似对象问题
- 缺点
  - 没有解决对象识别问题(即怎样知道一个对象的类型, 所有的对象都是Object实例, 而不能细化为其他子实例)

##### 构造函数模式

```javascript
function Person(name, age, job){
    this.name = name;
    this.age = age;
    this.job = job;
    this.sayName = function() {
        alert(this.name);
    };
}
var person1 = new Person('hanzhuo', 29, 'softwate Engineer')
var person2 = new Person('greg', 29, 'softwate Engineer')
```

- 优点

  - 没有显示地创建对象
  - 直接将属性和方法赋给了`this`对象
  - 没有`return`语句
  - 可是识别对象为`Person`类型

- 缺点

  - 每个方法都要在每个实例上重新创建一遍
  - 每定义一个函数, 也就是实例化了一个对象

  ```
  function Person(name, age, job){
      this.name = name;
      this.age = age;
      this.job = job;
      this.sayName =new Function() {
          alert(this.name);
      };  // 与声明函数在逻辑上是等价的
  }
  ```

- 可以将`sayName()`转移到构造函数外部

  ```javascript
  function Person(name, age, job){
      this.name = name;
      this.age = age;
      this.job = job;
     	this.sayName = sayName
  } 
    function sayName() {
          alert(this.name);
      };
  var person1 = new Person('hanzhuo', 29, 'softwate Engineer')
  var person2 = new Person('greg', 29, 'softwate Engineer')
  ```

  - 优点

    - 共享`sayName()`

  - 缺点

    - 在全局作用域中定义的函数在此时只能被某个对象调用, 让全局作用域优点名不副实

    - 如果对象要很多方法, 就要定义很多歌全局函数, 导致,没有封装性可言, 此时可用原型模式解决

- `constructor`

```javascript
alert(person1.constructor == Person); // true
alert(person2.constructor == Person); // true
```

- 检测对象类型(instanceof更可靠)

```javascript
alert(person1 instanceof Object) // true
alert(person1 instanceof Person) // true
alert(person2 instanceof Object) // true
alert(person2 instanceof Person) // true
```



##### 原型模式

```javascript
function Person(){
    
}
Person.prototype.name = 'Nicholas';
Person.prototype.age = 29;
Person.prototype.job = 'Software Engineer';
Person.prototype.sayName = function() {
	alert(this.name)
};

var person1 = new Person();
person1.sayName(); // 'Nicholas'

var person2 = new Person();
person2.sayName(); //'Nicholas'

alert(person1.sayName == person2.sayName) // true

```

![1538988509831](C:\Users\hanzhuo\AppData\Local\Temp\1538988509831.png)

- `isPrototypeOf()`

```javascript
alert(Person.prototype.isPrototypeOf(person1)) // true

alert(Person.prototype.isPrototypeOf(person2)) // true
```

- `Object.getPrototypeOf()`

```javascript
alert(Object.getPrototypeOf(person1) == Person.prototype) // true

alert(Object.getPrototypeOf(person1).name) // 'Nicholas'
```

- `hasOwnProperty()`

```javascript
function Person(){
    
}
Person.prototype.name = 'Nicholas';
Person.prototype.age = 29;
Person.prototype.job = 'Software Engineer';
Person.prototype.sayName = function() {
	alert(this.name)
};

var person1 = new Person();
var person2 = new Person();

alert(person1.hasOwnProperty('name'));

person1.name = 'Greg';
alert(person1.name); //'Greg'
alert(person1.hasOwnProperty('name')) // true
```

- 原型与`in`操作符

  - 两种方式使用`in`操作符
    - 在`for-in`循环中使用,
    - 单独使用时, `in`操作符会在通过对象能够访问给定属性时返回true, 无论改属性存在于实例中还是原型中

  ![1538989377143](C:\Users\hanzhuo\AppData\Local\Temp\1538989377143.png)

- `Object.keys()`
  - 取得所有可枚举的实例属性
  - 接收一个对象作为参数
  - 返回包含所有可枚举属性的字符串数组

```javascript
function Person(){
    
}
Person.prototype.name = 'Nicholas';
Person.prototype.age = 29;
Person.prototype.job = 'Software Engineer';
Person.prototype.sayName = function() {
	alert(this.name)
};

var keys = Object.keys(Person.prototype);
alert(keys); //'name, age,job,sayName'

var p1 = new Person();
p1.name = 'Rob';
p1.age = 31;
var p1keys = Object.keys(p1);
alert(p1keys); //'name,age'
```

- `Object.getOwnPropertyNames()`
  - 得到所有实例属性, 无论是否可枚举

```javascript
var keys = Object.getOwnPropertyNames(Person.prototype)
alert(keys); //'constructor,name,age,job,sayName'
```

- 更简单的原型语法

```javascript
function Person() {
    
}
Person.protorype = {
    name:'Nicholas',
    age: 29,
    job: 'software engineer',
    sayName: function(){
        alert(this.name)
    }
}
```

 - 注意点:

   - 此时的`constructor`不再指向`Person`, 而是指向`Object`构造函数
   - 用字面量的方式相当于新创建了一个对象, 这个对象也会自动获得constructor属性
   - `instanceof`还能返回正确结果

   ```
   var friend = new Person();
   alert(friend instanceof Object) // true
   alert(friend instanceof Person); // true
   alert(friend.constructor == Person) // false
   alert(friend.constructor == Object) // true
   ```

   - 如果`constructor`很重要, 可以特意设置为适当的值

   ```
   function Person() {
       
   }
   Person.protorype = {
   	constructor: Person /**/
       name:'Nicholas',
       age: 29,
       job: 'software engineer',
       sayName: function(){
           alert(this.name)
       }
   }
   ```

   - 这样设置会导致`[[Enumerable]]`为`true`, 默认情况下是不可以枚举的,此时可用`Object.defineProperty()`

   ```
   Object.defineProperty(Person.prototype, 'constructor',{
       enumerable: false,
       value: Person
   })
   ```

   - 原型模式的缺点
     - 所有的实例共享同样的属性, 当属性的值固定时, 所有的实例共享相同的值, 不能自定义属性的值.

##### 组合使用构造函数模式和原型模式

- 构造函数模式用于定义实例属性
- 原型模式用于定义方法和共享的属性

```javascript
function Person(name, age, job){
    this.name = name;
    this.age = age;
    this.job = job;
    this.friends = ['shelby', 'Court']
}

Person.prototype = {
    constructor: Person,
    sayName: function() {
        alert(this.name)
    }
}

var Person1 = new Person("Nicholas", 29, "soft")
var person2 = new Person('Greg', 27, 'doctor')

person1.friends.push('van');
alert(person1.friends); //'shelby, Count, Van'
alert(person2.friends); //'shelby,Count'
alert(person1.friends === person2.friends); // false
alert(person1.sayName === person2.sayName); // true
```

##### 动态原型模式

- 将所有信息都封装在了构造函数中
- 尽在必要的情况下初始化原型
- 保持了同时使用构造函数和原型的优点

```javascript
function Person(name, age, job){
    this.name = name;
    this.age = age;
    this.job = job;
    if(typeof this.sayName != 'function'){
        Person.prototype.sayName = function() {
            alert(this.name);
        }
    }
}

var friend = new Person('Nicholas', 29, 'software engineer')
friend.sayName();
```

- 以上代码中, 只在`sayName()`方法不存在的情况下, 才会将它添加到原型中
- 只会在初次调用构造函数时才会执行, 此后, 原型已经完成初始化, 不需要修改.
- 不必用`if`检查每个属性和方法, 只需检查其中一个即可.



##### 寄生构造函数模式

- 使用在前几种模式都不适用的情况下

```javascript
function Person(name, age, job){
    var o = new Object();
    o.name = name;
    o.age = age;
    o.job = job;
    o.sayName = function() {
		alert(this.name)
    }
    return o;
}

var friend = new Person('Nicholas', 29, 'soft')
friend.sayName(); // 'Nicholas'
```

- 简要说明上述例子

  - 除了使用`new`操作符并把使用的包装函数(`Person`)叫做构造函数之外, 和工厂模式一摸一样
  - 构造函数在不返回值的情况下, 默认会返回新对象实例
  - 添加`return`语句后, 可以重写调用构造函数时返回的值.

  - 项创建一个具有额外方法的特殊数组时, 由于不能直接修改`Array`构造函数, 可以使用这个模式

  ```javascript
  function SpecialArray() {
      /** 创建数组 **/
      var values = new Array();
      /** 添加值 **/
      /** 使用apply将数组里面的元素一个个push进数组, 如果不使用apply,就会将整个对象push进数组 **/
      values.push.apply(values, arguments);
      
      /**添加方法 **/
      values.toPipedString = function() {
          return this.join('|');
      }
      return values;
  }
  
  var colors = new SpecialArray('red', 'blue', 'green');
  alert(colors.toPipedString())  // 'red|blue|green'
  ```


##### 继承

------

- 给原型添加方法的代码要放在替换原型的语句之后

```javascript
function SuperType() {
    this.property = true;
}
SuperType.prototype.getSuperValue = function(){
    return this.property;
}

function SubType() {
    this.subproperty = false;
}

//继承了SuberType
SubType.prototype = new SuperType();

//添加新方法
SubType.prototype.getSubValue = function(){
    return this.subproperty;
}

//重写超类型中的方法
SubType.prototype.getSuperValue = function() {
    return false;
}

var instance = new SubType();
alert(instance.getSuperValue()); //false
```

- 实现继承时, 不能使用对象字面量创建原型方法, 这样做会重写原型链

```javascript
function SuperType() {
    this.property = true;
}
SuperType.prototype.getSuperValue = function(){
    return this.property;
}

function SubType() {
    this.subproperty = false;
}

//继承了SuberType
SubType.prototype = new SuperType();
//使用字面量添加新方法, 会导致上一行代码无效
SubType.prototype = {
    getSubValue: function(){
        return this.subproperty;
    },
    
    someOtherMethod: function(){
        return false;
    }
    
}
var instance = new SubType();
alert(instance.getSuperValue()); //error
```

- 原型链的问题
  - 共享属性的问题
  - 当一个实例向原型中添加属性值时, 该属性值会在另外一个实例当中反映出来

```javascript
function SuperType(){
	this.colors = ['red', 'blue', 'green'];
}
function SubType(){
    
}
//继承了SuperType
SubType.prototype = new SuperType();

var instance1 = new SubType();
instance1.colors.push('black');
alert(instance1.colors); //'red,blue,green,black'

var instance2 = new SubType();
alert(instance2.colors); //'red, blue, green,black'
```

###### 借用构造函数(constructor stealing)

- 伪造对象, 经典继承.
- 使用`apply()`和`call()`

```javascript
function SuperType(){
	this.colors = ['red', 'blue', 'green'];
}
function SubType(){
    //继承了SuperType
    SuperType.call(this)
}

var instance1 = new SubType();
instance1.colors.push('black');
alert(instance1.colors); //'red,blue,green,black'

var instance2 = new SubType();
alert(instance2.colors); //'red, blue, green'
```

- 以上代码注意点:
  - 新创建的`subType`下调用了`SuperType`构造函数
  - 在新`SubType`对象上执行`SuperType`函数中定义的所有度一项初始化代码
  - `SubType`的每个实例都会具有自己的`colors`副本

- 传递参数

```
function SuperType(name){
	this.name = name;
}
function SubType(){
    //继承了SuperType, 传递参数
    SuperType.call(this, 'Nicholas')
    
    // 实例属性
    this.age = 29;
}

var instance1 = new SubType();
alert(instance.name) //'Nicholas'
alert(instance.age) //29
```

###### 组合继承(伪经典继承)

- 原型链和构造函数的技术组合到一块

```javascript
function SuperType(name) {
    this.name = name;
    this.colors = ['red', 'blue', 'green']
}

SuperType.prototype.sayName = function(){
    alert(this.name)
}

function SubType(name, age){
    SuperType.call(this, name);
    
    this.age = age;
}

SubType.prototype = new SuperType();
SubType.prototype.sayAge = function(){
    alert(this.age);
}
var instance1 = new SubType('Nicholas', 29);
instance1.colors.push('black');
alert(instance1.colors); // 'red, blue, green, black'
instance1.sayName(); //'Nicholas'
instance1.sayAge(); //29

var instance2 = new SubType('Greg', 27);
alert(instance2.colors); // 'red, blue, green'
instance2.sayName(); //'Greg'
instance2.sayAge(); //27
```

###### 原型式继承

```javascript
function object(o){
    function F(){}
    F.prototype = o;
    return new F();
}
```

- 先创建一个临时性的构造函数
- 将传入的对象作为这个构造函数的原型
- 返回临时类型的一个新实例

```javascript
var person = {
    name: 'Nicholas',
    friends: ['shelby', 'court', 'van']
}

var anotherPerson = object(person)
anotherPerson.name = 'Greg';
anotherPerson.friends.push('Rob');

var yetAnotherPerson = object(person);
yetAnotherPerson.name = 'Linda';
yetAnotherPerson.friends.push('Barbie');
alert(person.friends) //'shelby, Court, Van, Rob,Barbie'
```

- `Object.create()`规范化了原型式继承

  - 在传入一个参数的情况下, `Object.create()`与`object()`方法的行为相同

  ```javascript
  var person = {
      name: 'Nicholas',
      friends: ['shelby', 'court', 'van']
  }
  
  var anotherPerson = Object.create(person)
  anotherPerson.name = 'Greg';
  anotherPerson.friends.push('Rob');
  
  var yetAnotherPerson = Object.create(person);
  yetAnotherPerson.name = 'Linda';
  yetAnotherPerson.friends.push('Barbie');
  alert(person.friends) //'shelby, Court, Van, Rob,Barbie'
  ```

  - 传入两个参数

  ```javascript
  var person = {
      name: 'Nicholas',
      friends: ['shelby', 'court', 'van']
  }
  
  var anotherPerson = Object.create(person, {
      name: {
          value: 'Greg'
      }
  })
  
  alert(anotherPerson.name);  //'Greg'
  ```

  ###### 寄生式继承

  ###### 寄生组合模式

  - 详情见《JavaScript高级程序设计》192页



### 函数表达式

------

#####  闭包

- 闭包是指有权访问另一个函数作用域中的变量的函数
- 创建闭包的常见方式, 就是在一个函数内部创建另一个函数

```javascript
function createComparisonFunction(propertyName){
    return function(object1, object2){
        value1 = object1[propertyName];
        value2 = object2[propertyName];
        if(value1 <value2){
            return -1;
        }else if(value1 > value2){
            return 1;
        } else {
            return 0;
        }
    }
}
```

- 例子解析
  - 匿名函数内部访问了外部变量`propertyName`
  - 匿名函数被返回了, 在其他地方调用时, 仍可以访问外部变量.
  - 之所以能访问, 是因为内部匿名函数的作用域链中包含`createComparisonFunction()`的作用域
- 函数第一次调用会发生什么?
  - 函数第一次被调用时, 会创建一个执行环境以及相应的作用域链
  - 把作用域链赋值给一个特殊的内部属性(即`[[Scope]]`)
  - 使用`this`, `arguments`和其他命名参数的值来初始化函数的活动对象
  - 在作用域链中, 外部函数的活动对象始终处于第二位, 外部函数的外部函数的活动对象处于第三位,直至作为作用域链终点的全局执行环境

- 闭包作用域链请看《JavaScript高级程序设计第三版》第197页

##### 闭包与变量

- 作用域链的副作用
  - 闭包只能取得包含函数中任何变量的最后一个值
  - 闭包所保存的是整个变量对象， 而不是某个特殊的变量

```javascript
function createFunctions() {
    var result = new Array();
    
    for(var i = 0; i < 10; i++){
        result[i] = function(){
            return i;
        };
    }
    return result;
}
```

- 例子解析

  - 会返回一个数组
  - 似乎每个函数都应该返回自己的索引值
  - 实际上, 每个函数都返回10
  - 每个函数的作用域链中都保存着`createFunction()`函数的活动对象
  - 它们引用的都是同一个变量i
  - 当`createFunctions()`函数返回后, 变量i的值是10
  - 此时每个函数都引用着保存变量i的同一个变量对象, 所以都是10
  - 但是,可以通过创建另一个匿名函数强制让闭包的行为符合预期

  ```javascript
  function createFunctions() {
      var result = new Array();
      
      for(var i = 0; i < 10; i++){
          result[i] = function(num){
          	return function(){
                  return num;
          	}
             
          }(i);
      }
      return result;
  }
  ```

  - 经过测试, 上面的代码会产生一些小问题

  ```javascript
  createFunctions()  // [ƒ, ƒ, ƒ, ƒ, ƒ, ƒ, ƒ, ƒ, ƒ, ƒ]
  
  /** 想要得到正确的结果, 得像下面这样写 **/
  
  for(var i = 0; i < 10; i++){
  	alert(createFunctions()[i]())
  }
  
  /** 正确的写法如下  **/
  function createFunctions() {
      var result = new Array();
      
      for(var i = 0; i < 10; i++){
          result[i] = function(num){
                  return num;
          }(i);
      }
      return result;
  }
  ```

##### 关于this对象

- [this指针详解(强烈推荐看一遍)](http://www.cnblogs.com/TomXu/archive/2012/01/17/2310479.html#!comments)

- 在闭包中使用`this`对象也可能会导致问题

- `this`对象时在运行时基于函数的执行环境绑定的

  - 在全局函数中, `this`等于`window`
  - 函数被某个对象调用时,`this`等于那个对象
  - 不过, 匿名函数的执行环境具有全局性
  - 因此, `this`通常指向`window`
  - 但有时候编写闭包的方式不同, 这一点可能不会那么明显

  ```
  var name = 'the window';
  
  var object = {
      name: 'my object',
      getNameFunc: function() {
          return function() {
              return this.name;
          }
      }
  }
  alert(object.getNameFunc()())  // 'the window' (在非严格模式下)
  ```

- 例子解析

  - 函数在调用时, 其活动对象都会自动取得两个特殊变量:`this`和`arguments`
  - 内部函数在搜索这两个变量时, 只会搜索到活动对象为止
  - 在上面的例子中`getNameFunc`被object调用, 其活动对象为object
  - 而匿名函数被windows 调用, 所以其活动对象为`Windows`, 相当于`window.(object.getNameFunc())()`
  - 可以将this对象保存在一个闭包能够访问到的变量里

  ```
  var name = 'the window';
  
  var object = {
      name: 'my object',
      getNameFunc: function() {
      	var that  = this;
          return function() {
              return that.name;
          }
      }
  }
  alert(object.getNameFunc()())  // 'my object' (在非严格模式下)
  ```

### BOM对象

------

##### window对象

- 窗口位置
  - `screenLeft`:窗口相对于屏幕左边的位置
  - `screenTop`:窗口相对于屏幕上边的位置
  - 火狐在`screenX`和`screenY`属性中提供相同的窗口位置,Safari和chrome也支持.在Opera中也支持这两个属性,但是与`screenLeft`和`screenTop`属性不对应, 建议不要在Opera中使用
  - 跨浏览器获取窗口左边和上边的位置

  ```javascript
  var leftPos = (typeof window.screenLeft == "number") ? window.screenLeft : window.screenX;
  
  var topPos = (typeof window.screenTop == "number") ? window.screenTop : window.screenY;
  
  代码解析:
  	在Firefox中,两个属性不存在,则取得screenX和screenY的值
  ```

![1540543601907](C:\Users\hanzhuo\AppData\Local\Temp\1540543601907.png)

- `moveTo`

  - 新位置的x和y值

- `moveBy`

  - 接收水平和垂直的像素值

  ```
  window.moveBy(-50, 0)
  
  这两个方法只在ie有效, 在其他浏览器都会被禁用
  ```

###### 窗口大小

![1540544151878](C:\Users\hanzhuo\AppData\Local\Temp\1540544151878.png)

```javascript
var pageWidth = window.innerWidth,
            pageHeight = window.innerHeight;

        /** 兼容ie8及更早 **/
        /** 如果pageWidth不存在 **/
        if (typeof pageWidth != 'number') {
            if (document.compatMode == "CSS1Compat") {
                pageWidth = document.documentElement.clientWidth;
                pageHeight = document.documentElement.clientHeight;
            } else {
                
                pageWidth = document.body.clientWidth;
                pageHeight = document.body.clientHeight;
            }
        }
        console.log(pageWidth, pageHeight)
```

###### 导航和打开窗口

- window.open()

- 参数

  - 要加载的url
  - 窗口目标
    - 该参数是已有框架或窗口的名称
    - 会在有该名称的窗口或框架中加载中加载第一个参数指定的URL 
    - 还可以是`_self` `_parent` `_top` `_blank`

  ```
  window.open("http://www.baidu.com", "topFrame")
  ```

  - 第三个参数是一个逗号分隔的设置字符串

  ![1540545887761](C:\Users\hanzhuo\AppData\Local\Temp\1540545887761.png)

```
window.open("http://www.baidu.com", "wroxWindow", "height=400,width=400,top=10,left=10,resizable=yes")
```

![1540546121151](C:\Users\hanzhuo\AppData\Local\Temp\1540546121151.png)



##### location对象

- 既是`window`对象的属性, 也是`document`对象的属性
- `window.location`和`document.location`引用的是同一个对象
- location对象的属性

![1540546299812](C:\Users\hanzhuo\AppData\Local\Temp\1540546299812.png)

###### 查询字符串参数

```javascript
       function getQueryStringArgs() {
           var qs = (location.search.length > 0 ? location.search.substring(1) : ""),
           args = {},
           items = qs.length ? qs.split("&") : [],
           item = null,
           name = null,
           value = null,
           i = 0,
           len = items.length;

           for(i = 0; i < len; i++){
               item = items[i].split("=");
               name = decodeURIComponent(item[0]);
               value = decodeURIComponent(item[1]);

               if(name.length) {
                   args[name] = value;
               }
           }
           return args;
       }
       getQueryStringArgs()
```

###### 位置操作

- `location.assgin`

  ```
  location.assgin("http://www.baidu.com")
  
  会生成一条新历史纪录替换原有的历史记录
  ```

- `window.location`

- `window.href`

```
window.location="http://www.baidu.com"
window.href="http://www.baidu.com"

也会调用assgin方法, 最常用的是设置href属性
```

- 修改`location`对象的其他属性也可以改变当前加载的页面

![1540547827397](C:\Users\hanzhuo\AppData\Local\Temp\1540547827397.png)

- `replace()`

  - 通过上述图片修改url后,浏览器的后退按钮仍然可用
  - 此方法是用来禁用浏览器的后退按钮的

  ```javascript
  setTimeout(function() {
      location.replace("http://www.baidu.com")
  }, 1000)
  
  -->一秒后将重定向到http://www.baidu.com, 后退按钮将处于禁用状态
  ```

- `reload()`

  ```
  location.reload();  //有可能从缓存中加载
  location.reload(true); // 从服务器重新加载
  ```



##### navigator对象

##### 检测插件

### DOM

------

##### DOM属性

- `getAttribute()`
  - 不属于`document`对象, 只能通过元素节点对象调用
- `setAttribute()`

```
object.getAttribute()
```

- `childNodes`属性
  - 返回一个数组

```javascript
element.childNodes
element.childNodes.length
```

```html
    <div id="container">
        <p>hanzhuo</p>
        <ul>
            <li class="choose a">1</li>
            <li class="choose">2</li>
            <li>3</li>
        </ul>
    </div>
    <script>
        var childNodes = document.getElementById("container").childNodes
        console.log(childNodes)  //[text, p, text, ul, text]
    </script>
注意:
	每次换行就相当于一个子节点text
	获取的只是第一层的子节点
```

- `nodeType`属性

  - 元素节点为1
  - 属性节点为2
  - 文本节点为3

  ```javascript
      <div id="container">
          <p>hanzhuo</p>
          <ul class="hanzhuo">
              <li class="choose a">1</li>
              <li class="choose">2</li>
              <li>3</li>
          </ul>
      </div>
      <script>
          var childNodes = document.getElementById("container").childNodes
          childNodes = Array.from(childNodes)
          var results = childNodes.filter((item) => {
               /* 获取到所有的元素节点 */
              return item.nodeType === 1
          })
          console.log(results)
      </script>
  ```

- `nodeValue`

  - 可以得到和改变文本节点的值

```javascript
    <div id="container">
        <p>
            hanzhuo
        </p>
        <ul class="hanzhuo">
            <li class="choose a">1</li><!DOCTYPE html>
            <li class="choose">2</li>
            <li>3</li>
        </ul>
    </div>
    <script>
        var childNodes = document.getElementById("container").childNodes
        childNodes = Array.from(childNodes)
        var results = childNodes.filter((item) => {
             /* 获取到所有的元素节点 */
            return item.nodeType === 1
        })
        /* results[0]为p标签, 不能直接获取p标签的nodeValue,此时将为null,p标签里面的文本其实是它的一个子节点里面的nodeValue的值 */
        results[0].childNodes[0].nodeValue = "哈哈"
    </script>
```

- `firstChild` 和`lastChild`属性
  - 访问子节点的第一个元素和最后一个元素

```
node.firstChild   =====    node.childNodes[0]
```

- `addLoadEvent()`
  - 页面加载完成之后执行多个函数
  - 好扩展

```javascript
addLoadEvent(func){
   var oldOnload = window.onload
    if(typeof window.onload !== "function") window.onload = func
    else{
        window.onload = function() {
            oldOnload()
            func()
        }
    }
}
addLoadEvent(first)
addLoadEvent(second)
```

- `parentNode`属性
  - 父节点
- `previousSibiling`  和 `nextSibling`
  - 包括文本节点
- `previousElementSibling`和 `nextElementSibling`
  - 只包括元素节点

![1540866875072](C:\Users\hanzhuo\AppData\Local\Temp\1540866875072.png)

- `hasChildNodes()`

  - 在包含一个或多个节点的时候返回`true`

- `appendChild()`

  - 向`childNodes`列表末尾添加一个节点

  - 返回新增的节点
  - 如果传入的节点已经是文档的一部分了, 会转移到新位置

  ```javascript
  var returnNewNode = someNode.appendChild(newNode)
  returnNewNode === newNode //true
  someNode.lastChild === returnNewNode //true
  ```

- `insertBefore()`

  - 两个参数:要插入的节点和作为参照的节点
  - 如果参照节点为空, 则插入末尾

- `replaceChild()`

  - 两个参数:要插入的节点和要替换的节点
  - 替换节点将由这个方法返回并从文档树中被移除, 同时由要插入的节点占据其位置

  ```
  // 替换第一个子节点
  var returnNode = someNode.replaceChild(newNode, someNode.firstChild)
  
  注意:
  	从技术上来讲, 被替换的节点仍然还在文档中, 但它在文档中已经没有了自己的位置
  ```

- `removeChild()`

  - 一个参数: 要移除的节点
  - 被移除的节点将成为方法的返回值
  - 仍然为文档所有, 只不过在文档中已经没有了自己的位置

- `cloneNode()`

  - 创建一个相同的副本
  - 参数为`true`, 深复制, 也就是复制节点和整个子节点树
  - 参数为`false`, 浅复制, 复制节点本身
  - 复制后返回的节点并没有被指定父节点, 需要重新添加到文档中

#####  document类型

- `document.documentElement`

  - 始终指向<HTML>元素
- `document.body`
  - 指向`body`元素
  - 所有浏览器都支持以上两种属性

- `document.title`

  ```
  取得标题
  var originalTitle = document.title;
  
  设置标题
  document.title = "haha"
  ```

- `document.forms`

  - 包含文档中所有的<form>元素

- `document.images`

  - 获取所有的<img>元素

- `document.links`

  - 获取所有单`href`属性的<a>元素


##### Element类型

- `attributes`

  - 保存一个元素的所有属性(包括自定义属性)
  - `getNamedItem(name)`: 通过name获取属性
  - `removeNamedItem(name)`
  - `setNamedItem(name)`
  - `item(pos)`: 返回位于数字pos位置处的节点

  ```
  aSec[0].attributes.getNamedItem('my-color') //my-color="red"
  
  
  ```

  - `attributes`里面的每个节点的`nodeValue`就是属性的值

  ```javascript
  var  id = element.attributes.getNamedItem('id').nodeValue
  var  id = element.attributes['id'].nodeValue
  ```

  - 也可以设置新值

  ```
  element.attributes['id'].nodeValue = 'someOtherId';
  ```



##### Text类型

- `nodeType`为3

- `nodeName`为`#text`(不是大写的text)

- `nodeValue`为包含的文本

- `parentNode`是一个`Element`

- 没有子节点

- 下列方法可以操作节点中的文本

  - `appendData(text)`: 将text添加到节点的末尾
  - `deleteData(offset, count)`: 在offset指定位置开始删除count个字符
  - `insertData(offset, text)`: 在offset处插入text
  - `replaceData(offset, count, text)`: 用text替换从offset指定位置到offset+count为止处的文本
  - `splitText(offset)`: 从offset处将当前文本节点分成两个文本节点
  - `substringData(offset, count)`: 提取从offset指定的位置到offset+count为止处的字符串
  - 文本节点还有一个`length`属性(nodeValue.length == data.length)

- 创建文本节点

  - `createTextNode`

  ```
  var textNode = document.createTextNode('hello world')
  element.appendChild(textNode)
  ```

- 规范化文本节点

  - DOM中存在相邻文本节点容易导致混乱,分不清哪个文本节点表示哪个字符串, 于是催生了合并相邻文本节点的方法
  - `normalize()`
    - 在父元素上调用时, 两个或多个文本节点会合并成一个节点, 结果节点的nodeValue等于其他文本节点的拼接值

  ```
  element.normalize()
  ```

##### DocumentFragment类型

- 轻量级文档
- 可以包含和控制节点
- 不会占用额外的资源
- 特征
  - `nodeType`: 11
  - `nodeName`: `#document-fragment`
  - `nodeValue`: null
  - `parentNode`: null
- 虽然不能讲文档片段直接添加到文档中, 但是可以作为一个仓库, 在里面保存将来可能会添加到文档中的节点

```
var fragment = document.createDocuemntFragment()

```

- 继承了`Node`的所有方法
- 如果将文档中的节点添加到文档片段中, 就会从文档树当中移除该节点
- 可以通过`appendChild`或`insetBefore`将文档片段中内容添加到文档中, 实际上只会将文档片段中的所有子节点添加到相应的位置上



### DOM扩展

------

##### 选择符API

- `querySelector()`

  - 返回与该模式匹配的第一个元素
  - 没有找到, 返回null
  - 只返回一个元素

  ```
  /** 取得body元素 **/
  var body = document.querySelector('body')
  
  var myDiv = document.querySelector('#myDiv')
  
  /** 取得类为selected的第一个元素
  var selected = document.querySelector('.selected')
  ```

- `querySelectorAll()`

  - 返回`NodeList`的实例



- `matchesSelector()`

  - 为Element类型新增方法
  - 接收css选择符参数
  - 如果调用元素与该选择符匹配, 返回`true`, 否则返回`false`

  ```javascript
  if(document.body.matchesSelector('body.page1')){
      // true
  }
  ```

  - 有兼容性, 包装方法

  ![1541658682755](C:\Users\hanzhuo\AppData\Local\Temp\1541658682755.png)

##### 元素遍历

- 对于元素减的空格, ie9之前不会返回文本节点, 其他浏览器会,这样,就导致了在使用`childNodes`和`firstChild`等属性的行为不一致, 所以定义了一组属性

- 为DOM元素添加的属性
  - `childElementCount`: 返回子元素(不包括文本节点和注释)的个数
  - `firstElementChild`: 指向第一个子元素
  - `lastElementChild`:指向第二个子元素
  - `previousElementSibling`: 指向前一个同辈元素
  - `nextElementSibling`:指向后一个同辈元素

- 遍历代码

```javascript
var i,
	len,
	child = element.firstElementChild;
while(child != element.lastElementChild){
    processChild()
    child = child.nextElementSibling
}
```



##### HTML5

------

###### 与类相关的扩充

- `classList`属性
  - `DOMTokenList`的实例
  - `add(value)`: 添加到列表, 存在不添加
  - `contains(value)`: 是否存在给定的值, 返回`true` or `false`
  - `remove(value)`: 删除
  - `toggle(value)`: 存在则删除, 不存在则添加

###### 焦点管理

- `document.activeElement`

  - 是一个属性
  - 引用DOM中获得了焦点的元素

  ```javascript
  var button = document.getElementById('myButton')
  button.focus();
  alert(document.activeElement === button); //true
  ```

  - 默认情况下, 刚刚加载时保存的是body元素的引用, 文档加载期间为`null`

- `hasFocus()`

  - 是方法
  - 确定文档是否获得了焦点

  ```javascript
  var button = document.getElmentById('myButton')
  button.focus()
  alert(document.hasFocus) // true
  ```



###### HTMLDocument的变化

- `readyState`属性

  - `loading`:正在加载文档
  - `complete`: 已经加载完文档

  ```
  if(document.readyState === "compelete"){
      //
  }
  ```


















