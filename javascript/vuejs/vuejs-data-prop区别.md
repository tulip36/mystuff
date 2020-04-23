# method，watch 介绍

[![](https://upload.jianshu.io/users/upload_avatars/5657049/ca730c54-2460-434b-9405-46c225d3a377?imageMogr2/auto-orient/strip|imageView2/1/w/96/h/96/format/webp)](https://www.jianshu.com/u/a2660ca241bd)

[vivi\_0833](https://www.jianshu.com/u/a2660ca241bd)关注

0.0142018.02.12 04:05:09字数 511阅读 2,263

### data, prop, computed, method 的区别

| 类型 | 加载顺序 | 加载时间 | 写法 | 作用 | 备注 |
| --- | --- | --- | --- | --- | --- |
| prop | 1 | beforeCreated, created之间 | 对象或数组 | 接收父组件传递的值 |  |
| data | 3 | 同↑ | 对象或函数 | 定义以及初始化数据 | 最好是用于视图上展示的数据，否则最好定义在外面或者vm对象内（减少开支，提高性能）；组件内只接受函数 |
| computed | 4 | 同↑ | 函数 | 提供相对简单的数据计算 |
| method | 2 | 同↑ | 函数 | 提供相对复杂的数据计算 |  |

## data 写法注意

![](https://upload-images.jianshu.io/upload_images/5657049-f98a7b09af639eb3?imageMogr2/auto-orient/strip|imageView2/2/w/318/format/webp)

image

![](https://upload-images.jianshu.io/upload_images/5657049-283d13b28fbe90fa?imageMogr2/auto-orient/strip|imageView2/2/w/283/format/webp)

image

### data 与 computed 的关系

> 根据官网的介绍，虽然模板内的表达式很方便，但是对于任何复杂的逻辑，你都应当使用计算属性。

data 只是对于你想要展示的数据的定义，但是，如果该数据需要进行复杂的处理（例如将其变为翻转字符串等），就需要计算属性的帮忙。

| 类型 | 作用 | 备注 |
| --- | --- | --- |
| data | 定义以及展示数据 |  |
| computed | 对数据进行复杂的操作转换 |  |

```kotlin
<span>{{reversedMessage}}</span>
data() {
  message: '',
},
computed: {
  reversedMessage() {
    return this.message.split('').reverse().join('');
  },
},

```

---

### 自己给自己的挖坑历史：

![](https://upload-images.jianshu.io/upload_images/5657049-a03a5a4cf712c092?imageMogr2/auto-orient/strip|imageView2/2/w/756/format/webp)

image

事情是这样的：最开始 data 内声明了 xAxisData 和 ratioLineOption（option是对象，里面包括前者） ，**事实证明—— xAxisData改变了也不会影响option(尽管里面包含{data: this.xAxisData}，只有重新声明改变option才行)**
所以后来我把option写在了conputed里面，如果里面有值（不包括对象）改变的话，option都会自动更新改变。

---

### computed 与 method 的区别

当然，我们可以把同一函数定义为一个方法而不是计算属性，两种方式最后的结果一样的，不同的是，计算属性是基于他们的依赖进行缓存的，只有相关依赖的值发生改变才会重新求值；而方法只要被触发就会再次执行该函数。如果你不希望有缓存，请用方法来代替。

| 类型 | 是否被缓存 | 备注 |
| --- | --- | --- |
| computed | 是 | 只要依赖值有变化就会立马执行 |
| method | 否 | 需要绑定事件 |

```kotlin
method: {
  reversedMessage() {
    return this.message.split('').reverse().join('');
  },
},

```

### computed 与 watch 的区别

在很多情况下，computed 会比 watch 使用起来更加方便，但是当需要在数据变化时执行异步或者开销比较大的情况下，用 watch 会更加合适。

例如官网提供的例子（问与答）。
watch 观察 question 的值，若值有改变会执行方法 getAnswer，并且根据 question 不同的值，answer 会给出不同的回答，并且会异步调用 API 返回相应的值，这些都是计算属性做不到的。

| 类型 | 目的 | 备注 |
| --- | --- | --- |
| computed | 依赖变动实时更新数据 | 更新数据 |
| watch | 观察某一特定的值，执行特定的函数 | 观察数据 |

```jsx
<div id="watch-example">
  <p>
    Ask a yes/no question:
      <input v-model="question">
  </p>
  <p>{{answer}}</p>
</div>

var watchExampleVM = new Vue({
  el: "watch-example",
  data: {
    question: '',
    answer: 'I cannot give you an answer until you ask a question!',
  },
  watch: {
    question: function(newquestion, oldQuestion) {
      this.answer = 'Waiting for you to stop typing';
      this.getAnswer();
    },
  },
  method: {
    getAnswer: _.debounce{
      function() {

        if (this.question.indexOf('?') === -1) {
          this.answer = 'Question ususally contain a question mark -- ?';
        }
        this.answer = 'Thinking';
        var vm = this.axios.get(XXX)
        ` ` `  ` ` `
      },
      500
    },
  },
})

```

### watch观察数据栗子

![](https://upload-images.jianshu.io/upload_images/5657049-ee166f30cb94c86a?imageMogr2/auto-orient/strip|imageView2/2/w/595/format/webp)
