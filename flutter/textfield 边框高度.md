## Flutter：修改TextField的高度，以及无边框圆角

修改TextField的高度可以通过decoration: InputDecoration的**contentPadding**进行修改，代码如下

```
new TextField(
          decoration: InputDecoration(
            contentPadding: const EdgeInsets.symmetric(vertical: 10.0),
          ),
        )
```

### 这种修改可以在没有prefixIcon的时候生效，如果加入prefixIcon，就会出现一个最小的高度，这时，按照如上方法修改如果高度较小的时候会修改失败。

因而需要再TextField外层加一个**BoxConstraints**，代码如下：


```
new ConstrainedBox(
        constraints: BoxConstraints(
          maxHeight: 25,
          maxWidth: 200 ),
        child: new TextField(
          decoration: InputDecoration(
            contentPadding: const EdgeInsets.symmetric(vertical: 4.0),
            hintText: '请输入搜索内容',
            prefixIcon: Icon(Icons.search), // contentPadding: EdgeInsets.all(10),
 border: OutlineInputBorder(
                borderRadius: BorderRadius.circular(15),
                borderSide: BorderSide.none),
            filled: true,
            fillColor: Color(0xffaaaaaa),
          ),
        ),
      ),

```

maxHeight为最大高度，可酌情进行更改，实际修改的高度依旧是contentPadding这个属性。

maxWidth为最大宽度，可修改TextField的宽度。