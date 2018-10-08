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
    - 返回妹子函数调用的结果组成的数组

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



















































































