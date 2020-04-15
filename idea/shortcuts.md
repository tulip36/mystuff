### 1. 编辑器代码输入快捷键

#### 1.1 for 语句

```
iter    Iterate (for each..in) 
itin    Iterate (for..in) 
itli    Iterate over a List
itar    Iterate elements of array 
ritar   Iterate elements of array in reverse order 
```

#### 1.2 当光标处在（）里面时， 按alt + shift + v  添加本地变量到等式前面
```
before: userService.getOne(queryWrapper);
after: User user = userService.getOne();
```
#### 1.3  当光标处在（）里面时， 按alt + enter  添加本地变量到前一个语句
```
before: userService.getOne(queryWrapper);
after: QueryWrapper queryWrapper = new QueryWrapper();
		userService.getOne(queryWrapper);
```




### 2. 工具栏快捷键

#### 2.1 Hierarchy class view

```java
Ctrl + H
```




