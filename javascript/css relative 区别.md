# CSS \- 定位属性position使用详解（static、relative、fixed、absolute）

2017\-09\-03 发布：hangge 阅读：10001

## 一、position 属性介绍

（1）position 属性自 CSS2 起就有了，该属性规定元素的定位类型。所有主流浏览器都支持 position 属性。

（2）position 的可选值有四个：static、relative、absolute、 fixed。下面分别进行介绍。（其实还有个 inherit，不过这个是 IE 特有的，这里就不做讨论）

## 二、position: static（默认值）

### 1，基本介绍

（1）static 是默认值。表示没有定位，或者说不算具有定位属性。

（2）如果元素 position 属性值为 static（或者未设 position 属性），该元素出现在正常的流中（忽略 top, bottom, left, right 或者 z\-index 声明）。

### 2，使用样例

```

<style>
  div {
    width: 200px;
    height: 100px;
    background-color: #C9FFFF;
  }
</style>
 
<div></div>
<input type="text"/>

 ```

我们不设置元素的 postion 属性值，那么默认的显示效果如下：

[![原文:CSS - 定位属性position使用详解（static、relative、fixed、absolute）](https://www.hangge.com/blog_uploads/201708/2017082720525381093.png)](#)

## 三、position: relative（相对定位）

### 1，基本介绍

（1）relative 生成相对定位的元素，相对于其正常位置进行定位。

（2）相对定位完成的过程如下：

*   首先按默认方式（static）生成一个元素(并且元素像层一样浮动了起来)。
*   然后相对于以前的位置移动，移动的方向和幅度由 left、right、top、 bottom 属性确定，偏移前的位置保留不动。

### 2，样例代码

下面代码将文本输入框 position 设置为 relative（相对定位），并且相对于默认的位置向右、向上分别移动 15 个像素。

```
<style>
  div {
    width: 200px;
    height: 100px;
    background-color: #C9FFFF;
  }
   
  input {
    position: relative;
    left: 15px;
    top: -15px;
  }
</style>
 
<div></div>
<input type="text" />
```

运行效果如下：

[![原文:CSS - 定位属性position使用详解（static、relative、fixed、absolute）](https://www.hangge.com/blog_uploads/201708/2017082720542782867.png)](#)

## 四、position: absolute（绝对定位）

### 1，基本介绍

（1）absolute 生成绝对定位的元素。

（2）绝对定位的元素使用 left、right、top、bottom 属性相对于其最接近的一个具有定位属性的父元素进行绝对定位。

（3）如果不存在这样的父元素，则相对于 body 元素，即相对于浏览器窗口。

### 2，样例代码

*   下面代码让标题元素相对于它的父容器做绝对定位（注意父容器 position 要设置为 relative）。
*   同时通过 top 属性让标题元素上移，使其覆盖在父容器的上边框。
*   最后通过 left 和 margin\-left 配合实现这个绝对定位元素的水平居中。

```
<style>
  #box {
    width: 200px;
    height: 100px;
    -webkit-box-flex:1;
    border: 1px solid #28AE65;
    border-radius:6px;
    padding: 20px;
    position: relative;
    font-size: 12px;
  }
 
  #title {
    background: #FFFFFF;
    color: #28AE65;
    font-size: 15px;
    text-align: center;
    width: 70px;
    height: 20px;
    line-height: 20px;
    position: absolute;
    top: -10px;
    left: 50%;
    margin-left: -35px;
  }
</style>
 
<div id="box">
  <div id="title">标题</div>
  欢迎访问 hangge.com 欢迎访问 hangge.com 欢迎访问 hangge.com 欢迎访问 hangge.com
</div>
```

运行效果如下，标题元素虽然是在边框容器的内部。但由于其使用绝对定位，并做位置调整，最后显示效果就是覆盖在父容器边框上。

[![原文:CSS - 定位属性position使用详解（static、relative、fixed、absolute）](https://www.hangge.com/blog_uploads/201708/2017082720570690698.png)](#)

## 五、position: fixed（固定定位）

### 1，基本介绍

（1）fixed 生成绝对定位的元素，该元素相对于浏览器窗口进行定位。

（2）固定定位的元素不会随浏览器窗口的滚动条滚动而变化，也不会受文档流动影响，而是始终位于浏览器窗口内视图的某个位置。

### 2，样例代码

（1）下面代码让输入框位于浏览器窗口的底部。

```
<style>
  input {
    position: fixed;
    bottom: 10px;
  }
</style>
 
<ol>
  <li>数据</li><li>数据</li><li>数据</li><li>数据</li><li>数据</li><li>数据</li>
  <li>数据</li><li>数据</li><li>数据</li><li>数据</li><li>数据</li><li>数据</li>
  <li>数据</li><li>数据</li><li>数据</li><li>数据</li><li>数据</li><li>数据</li>
  <li>数据</li><li>数据</li><li>数据</li><li>数据</li><li>数据</li><li>数据</li>
</ol>
<input type="text" />
```

（2）可以看到不管滚动条如何滚动，输入框始终处于窗口的最下方。

    [![原文:CSS - 定位属性position使用详解（static、relative、fixed、absolute）](https://www.hangge.com/blog_uploads/201708/2017082721011046663.png)](#)       [![原文:CSS - 定位属性position使用详解（static、relative、fixed、absolute）](https://www.hangge.com/blog_uploads/201708/2017082721011762210.png)](#)
