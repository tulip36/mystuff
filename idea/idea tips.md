### 1. idea 文件名颜色所代表的含义

| 颜色 | 加入版本控制 | 提交 | 改动 |
| ---- | :----------- | ---- | ---- |
| 绿色 | Yes          | No   |      |
| 白色 | Yes          | Yes  | No   |
| 蓝色 | Yes          | Yes  | Yes  |
| 灰色 | 忽略         |      |      |
| 红色 | No           |      |      |



红色，未加入版本控制；
蓝色，加入版本控制，已提交，有改动；
白色，加入版本控制，已提交，无改动；
灰色：版本控制已忽略文件。

### 2. IDEA] 文件修改提示

```java
Settings -> Editor -> General -> Editor Tabs: Check "Markmodified tabs with asterisk"
```



### 3. 自动保存功能

IntelljJ IDEA关于文件自动保存功能主要有两种方式：

- 切换到其他应用时保存变化（默认使能）
```
  设置路径：Settings -> Apperance & Behavior -> Save files onframe 
deactivation
```
- 如果应用空闲则自动保存变化（默认禁止）

```
  设置路径：Settings -> Apperance & Behavior -> Save filesautomatically if application is idle for ... sec.
```