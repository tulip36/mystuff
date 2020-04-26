# Flutter布局之Stack重叠控件

[![](https://upload.jianshu.io/users/upload_avatars/679754/efeafe645236.jpg?imageMogr2/auto-orient/strip|imageView2/1/w/96/h/96/format/webp)](https://www.jianshu.com/u/56300861aba5)

[TryEnough](https://www.jianshu.com/u/56300861aba5)关注

0.7692019.01.07 02:38:56字数 172阅读 5,377

## 效果图


![](images/md-2020-04-25-14-23-19.png)

TryEnough

## 代码

```dart
import 'package:flutter/rendering.dart' show debugPaintSizeEnabled;
import 'package:flutter/material.dart';

void main() {
//  debugPaintSizeEnabled = true;
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: MyHomePage(title: 'Flutter Demo Home Page'),
    );
  }
}

class MyHomePage extends StatefulWidget {
  MyHomePage({Key key, this.title}) : super(key: key);

  final String title;

  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  @override
  Widget build(BuildContext context) {
    //关键代码
    var stack = new Stack(
      alignment: const Alignment(0.0, 0.6),  //分析 2
      children: [
        new CircleAvatar(   //分析 3
          backgroundImage: new AssetImage('images/lake.jpg'),
          radius: 100.0,
        ),
        new Container(   //分析 4
          decoration: new BoxDecoration(
            color: Colors.black45,
          ),
          child: new Text(
            '添加水印',
            style: new TextStyle(
              fontSize: 20.0,
              fontWeight: FontWeight.bold,
              color: Colors.white,
            ),
          ),
        ),
      ],
    );
    return Scaffold(
      appBar: AppBar(
      title: Text(widget.title),
      elevation: 5.0,
    ),
      body: Center(  //分析 1
        child: stack,
      ),
    );
  }
}

```

## 分析

*   1.  在屏幕中央添加一个stack
*   2.  Stack中第一个widget为底部的内容，第二个为盖在上面的widget。所以这里的圆形图片CircleAvatar是底部，第二个Container为盖在上面的文字。那么分析2这里的alignment就是调整第二个widget位置的属性。Alignment将第一个widget的中心当作（0，0）坐标。所以这里的（0.0，0.6）就是如图的位置。
*   3.  CircleAvatar是画圆形图的widget，当使用图时，应该指定backgroundImage属性，同时可以设置半径。
*   4.  这个代表盖在底部图片上的文字