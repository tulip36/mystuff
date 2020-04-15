### 1. Thymeleaf 使用非严格HTML5

解决spring-boot thymeleaf模板对非严格HTML5格式文件的解析
原创isonre77 最后发布于2017-12-21 14:06:38 阅读数 7573  收藏
展开
在使用springboot的过程中，如果使用thymeleaf作为模板文件，则要求HTML格式必须为严格的html5格式，必须有结束标签，否则会报错！解决办法如下：

1、你可以使用严格的标签，也就是每个标签都有结束标签。
比如你在使用Vue.js这样的库，然后有

```html
<div v-cloak></div>

这样的html代码，也会被thymeleaf认为不符合要求而抛出错误。
这种方式可能会比较麻烦，每次都需要手动添加。
```

2、在application.properties中增加

```xml
spring.thymeleaf.content-type=text/html 
spring.thymeleaf.cache=false 
spring.thymeleaf.mode =LEGACYHTML5
```


即声明thymeleaf使用非严 格的html。启动之后访问页面会报如下错误：

```java
Cannot perform conversion to XML from legacy HTML: The nekoHTML library is not in classpath. 
    nekoHTML 1.9.15 or newer is required for processing templates in "LEGACYHTML5" mode [http://nekohtml.sourceforge.net]. Maven spec: "net.sourceforge.nekohtml::nekohtml::1.9.15". IMPORTANT: DO NOT use versions of nekoHTML older than 1.9.15.

```




修改pom.xml 添加以下依赖

```xml
<dependency>
  <groupId>org.codelibs</groupId>
  <artifactId>nekohtml</artifactId>
  <version>2.1.0</version>
</dependency>
```

