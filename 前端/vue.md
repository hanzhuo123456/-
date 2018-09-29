### `watch`深度监听

- 当watch去监听一个引用类型时会显得力不从心, 监听不到, 此时就需要使用深度监听了

  ```javascript
  <script>
    var App = {
      template: "<div><input v-model='arr[0].name' type='text'/><span>{{ arr[0].name }}</span></div>",
      data: function () {
        return {
          message: "你好啊!",
          arr: [{'name': "hanzhuo"}]
        }
      },
      watch: {
        message: function (dataStr) {
          console.log(dataStr)
        },
        arr: function () {
          //此时并不会打印
          alert("a")
        }
      }
    };
    var vm = new Vue({
      el: '#app',
      components: {
        app: App
      },
      template: '<app/>'
    });
  
  </script>
  ```

- 深度监听代码如下

  ```js
     watch: {
        message: function (dataStr) {
          console.log(dataStr)
        },
        arr: {
          deep: true,
          handler: function () {
            console.log("aa")
          }
        }
      }
  ```

### 生命周期

```js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>生命周期</title>
  <script src="https://cdn.bootcss.com/vue/2.4.2/vue.js"></script>
  <script src="https://unpkg.com/vuex@3.0.1/dist/vuex.js"></script>
</head>
<body>
<div id="app">

</div>
<script>
  var Son = {
    template: "<h1>son</h1>"
  };
  var App = {
    template: "<div><son v-if='isExist'></son><button @click='isExist=!isExist'>创建与销毁</button></div>",
    data: function () {
      return {
        message: "你好啊!",
        isExist: false
      }
    },
    beforeCreate: function(){
      // 创建组件之前
      console.log(this.message);    // undefined
    },
    created:function () {
      // 创建组件之后
      console.log(this.message);    //你好啊!
    },
    // 使用该组件, 就会触发以上的事件(钩子函数)
    // created中可以操作数据... 并且可以实现vue-->html页面的影响,  应用: 发起ajax请求
     beforeMount: function(){
        // 原始DOM还没有被vue重新渲染之前
       //也就是VUE里面的template还没有替代原始的<div id="app"></div>
       // console.log(document.body.innerHTML);
     },
    mounted: function(){
      // 原始DOM还没有被vue重新渲染之后
      //也就是VUE里面的template替代了原始的<div id="app"></div>
      // mounted只执行一次
      // console.log(document.body.innerHTML);
    },
    // 以下两个是基于数据的改变
    // 当数据没有发生改变时, 并不会调用, 而mounted和beforeMount则一定会调用
    beforeUpdate: function(){
      console.log("beforeUpdate")
    },
    updated: function(){
      console.log("updated")
    },
    components: {
      son: Son
    },
  };
  var vm = new Vue({
    el: '#app',
    components: {
      app: App
    },
    template: '<app/>'
  });

</script>
</body>
</html>

```

### jsonp跨域请求

- network得到数据但是控制台打印不出来的原因

  - 格式不对, 需要后台指定callback
  - [https://blog.csdn.net/linli1991/article/details/73064806/](https://blog.csdn.net/linli1991/article/details/73064806/)


