## 1. Mybatis 与 Mybatis plus 对应应用程序设置的主要区别

### 1.1 主要内容对比

| 序列   | 目录   | 内容     | mybatis      |mybatis plus  |说明 |
| :-----: | :----------: |:--: | :-----: | :------ | ------- |
| 1 | resources | mybatis-config.xml | x | |1. 配置数据源，2.  mapper |
| 2 | resources | application.yml |  |x |配置数据源 |
| 3 | pojo | User.java | x |x |实体类 |
| 4 | dao | UserMapper.java | x | |接口类 |
| 5 | dao | UserMapper.xml | x | |构造查询语句 |
| 6 | mapper | UserMapper.java |  |x |接口类, 继承至BaseMapper,拥有各种预定义的查询方法 |
|  |  |  |  | | |
|  |  |  |  | | |
|  |  |  |  | | |

### 2. Mybatis 具体的代码

#### 2.1 mybatis-config.xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.cj.jdbc.Driver"/>
                <property name="url"
                          value="jdbc:mysql://localhost:3306/warehouse?useSSL=true&amp;useUnicode=true&amp;characterEncoding=UTF-8"/>
                <property name="username" value="jason"/>
                <property name="password" value="Bec-5369-34xmax"/>
            </dataSource>
        </environment>

    </environments>
    <mappers>
        <mapper resource="com/example/mybatisdemo/dao/BusCustomerMapper.xml"/>
    </mappers>
</configuration>
```



#### 2.2 User.java 实体类

```java
package com.example.mybatisplusdemo.pojo;

import lombok.Data;

@Data
public class User {
    private Long id;
    private String name;
    private Integer age;
    private String email;
}

```



#### 2.3 UserMapper.java 接口类

```java
public interface UserMapper {
    List<User> getUserList();
}

```

#### 2.4 UserMapper.xml 构造查询语句

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.example.mybatisdemo.dao.BusCustomerMapper">
    <select id="getBusCustomerList"  resultType="com.example.mybatisdemo.pojo.BusCustomer">
        select * from warehouse.bus_customer;
    </select>
</mapper>
```

### 3. Mybatis plus 具体的代码

#### 3.1 application.yml

```yaml
# DataSource Config
spring:
  datasource:
      driver-class-name: com.mysql.cj.jdbc.Driver
      url: "jdbc:mysql://localhost:3306/warehouse"
      username: jason
      password: Bec-5369-34xmax
```

#### 3.2 User.java 实体类

```java
package com.example.mybatisplusdemo.pojo;

import lombok.Data;

@Data
public class User {
    private Long id;
    private String name;
    private Integer age;
    private String email;
}
```

#### 3.3 UserMapper.java 接口类

```java
public interface UserMapper extends BaseMapper<User> {
}
```