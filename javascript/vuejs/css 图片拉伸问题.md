
## 多个图片统一大小后的拉伸问题
![](/images/2020-04-23-16-17-49.png)

## 解决办法

- background-size: cover 
  - 来避免对图片造成的压缩或者拉伸。
  
- object-fit: cover;


## 效果图
![](/images/2020-04-23-16-20-09.png)

## Object-fit 具体属性

| 属 性   |	描  述|
|:------|:--- |
| fill|	默认值。整个对象将完全填充此框。 如果对象的高宽比不匹配其框的宽高比，那么该对象将被拉伸以适应。|
|contain	|整个对象在填充盒子的同时保留其长宽比，因此如果宽高比与框的宽高比不匹配，该对象将被添加“黑边”。|
|cover |	被替换的内容大小保持其宽高比，同时填充元素的整个内容框。 如果对象的宽高比与盒子的宽高比不匹配，该对象将被剪裁以适应。|
|none	|内容尺寸不会被改变。|
|scale-down	|内容的尺寸就像是指定了none或contain，默认应用尺寸最小的值|

## 代码

```
<div>
    <img src="./public/test.jpg" class="initImg"/> 
    <p>图片初始化</p>
</div>

<div>
    <img src="./public/test.jpg" class="initImg fillImg"/> 
    <p>object-fit:fill</p>
</div>

<div>
    <img src="./public/test.jpg" class="initImg containImg"/> 
    <p>object-fit:contain</p>
</div>
</br>

<div>
    <img src="./public/test.jpg" class="initImg coverImg"/> 
    <p>object-fit:cover</p>
</div>

<div>
    <img src="./public/test.jpg" class="initImg noneImg"/> 
    <p>object-fit:none</p>
</div>

<div>
    <img src="./public/test.jpg" class="initImg scaleDownImg"/> 
    <p>object-fit:scale-down</p>
</div>


//css
body div{
    display: inline-block;
    text-align: center;
}
.initImg{
    width: 150px;
    height: 80px;
}
.fillImg{
    object-fit: fill;
}
.containImg{
    object-fit: contain;
}
.coverImg{
    object-fit: cover;
}
.noneImg{
    object-fit: none;
}
.scaleDownImg{
    object-fit: scale-down;
}
```

## Object-fit 各个属性的效果图

![](/images/2020-04-23-16-23-33.png)