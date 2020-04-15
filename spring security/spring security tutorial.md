# [springsecurity整合springboot实现简单认证授权](https://www.cnblogs.com/ifme/p/12184433.html)

> 主要用到了springboot,springsecurity,mybatis,jsp

### 1. 创建项目

使用`idea`中的`spring`工具创建项目创建时勾选`springboot start web`和`springsecurity`最终生成的`pom.xml`文件如下

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.2.2.RELEASE</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>
    <groupId>com.example</groupId>
    <artifactId>springboot_security_jsp</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <packaging>war</packaging>
    <name>springboot_security_jsp</name>
    <description>Demo project for Spring Boot</description>

    <properties>
        <java.version>1.8</java.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-security</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.security</groupId>
            <artifactId>spring-security-taglibs</artifactId>
            <version>5.2.1.RELEASE</version>
        </dependency>
        <!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.48</version>
        </dependency>
        <!-- https://mvnrepository.com/artifact/tk.mybatis/mapper-spring-boot-starter -->
        <dependency>
            <groupId>tk.mybatis</groupId>
            <artifactId>mapper-spring-boot-starter</artifactId>
            <version>2.1.5</version>
        </dependency>


        <!--        整合jsp需要如下两个包-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-tomcat</artifactId>
        </dependency>
        <dependency>
            <groupId>org.apache.tomcat.embed</groupId>
            <artifactId>tomcat-embed-jasper</artifactId>
            <version>9.0.30</version>
        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
            <exclusions>
                <exclusion>
                    <groupId>org.junit.vintage</groupId>
                    <artifactId>junit-vintage-engine</artifactId>
                </exclusion>
            </exclusions>
        </dependency>
        <dependency>
            <groupId>org.springframework.security</groupId>
            <artifactId>spring-security-test</artifactId>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>jstl</groupId>
            <artifactId>jstl</artifactId>
            <version>1.2</version>
        </dependency>
        <dependency>
            <groupId>javax.annotation</groupId>
            <artifactId>jsr250-api</artifactId>
            <version>1.0</version>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>

</project>
```

### 2. 数据库表字段信息

```sql
CREATE TABLE `persistent_logins` (
  `username` varchar(64) NOT NULL,
  `series` varchar(64) NOT NULL,
  `token` varchar(64) NOT NULL,
  `last_used` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
  PRIMARY KEY (`series`)
) ENGINE=InnoDB DEFAULT CHARSET=latin1;

CREATE TABLE `sys_permission` (
  `ID` int(11) NOT NULL AUTO_INCREMENT COMMENT '编号',
  `permission_NAME` varchar(30) DEFAULT NULL COMMENT '菜单名称',
  `permission_url` varchar(100) DEFAULT NULL COMMENT '菜单地址',
  `parent_id` int(11) NOT NULL DEFAULT '0' COMMENT '父菜单id',
  PRIMARY KEY (`ID`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

CREATE TABLE `sys_role` (
  `ID` int(11) NOT NULL AUTO_INCREMENT COMMENT '编号',
  `ROLE_NAME` varchar(30) DEFAULT NULL COMMENT '角色名称',
  `ROLE_DESC` varchar(60) DEFAULT NULL COMMENT '角色描述',
  PRIMARY KEY (`ID`)
) ENGINE=InnoDB AUTO_INCREMENT=10 DEFAULT CHARSET=utf8;

CREATE TABLE `sys_role_permission` (
  `RID` int(11) NOT NULL COMMENT '角色编号',
  `PID` int(11) NOT NULL COMMENT '权限编号',
  PRIMARY KEY (`RID`,`PID`),
  KEY `FK_Reference_12` (`PID`),
  CONSTRAINT `FK_Reference_11` FOREIGN KEY (`RID`) REFERENCES `sys_role` (`ID`),
  CONSTRAINT `FK_Reference_12` FOREIGN KEY (`PID`) REFERENCES `sys_permission` (`ID`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

CREATE TABLE `sys_user` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `username` varchar(32) NOT NULL COMMENT '用户名称',
  `password` varchar(120) NOT NULL COMMENT '密码',
  `status` int(1) DEFAULT '1' COMMENT '1开启0关闭',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=6 DEFAULT CHARSET=utf8;

CREATE TABLE `sys_user_role` (
  `UID` int(11) NOT NULL COMMENT '用户编号',
  `RID` int(11) NOT NULL COMMENT '角色编号',
  PRIMARY KEY (`UID`,`RID`),
  KEY `FK_Reference_10` (`RID`),
  CONSTRAINT `FK_Reference_10` FOREIGN KEY (`RID`) REFERENCES `sys_role` (`ID`),
  CONSTRAINT `FK_Reference_9` FOREIGN KEY (`UID`) REFERENCES `sys_user` (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

### 3. 创建角色 pojo对象

这里直接使用`SpringSecurity`的角色规范

```java
package com.example.springboot_security_jsp.domain;

import com.fasterxml.jackson.annotation.JsonIgnore;
import org.springframework.security.core.GrantedAuthority;

/**
 * @author john
 * @date 2020/1/11 - 20:12
 */
public class SysRole implements GrantedAuthority {
    private Integer id;
    private String roleName;
    private String roleDesc;

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getRoleName() {
        return roleName;
    }

    public void setRoleName(String roleName) {
        this.roleName = roleName;
    }

    public String getRoleDesc() {
        return roleDesc;
    }

    public void setRoleDesc(String roleDesc) {
        this.roleDesc = roleDesc;
    }

    //标记此属性不做json处理
    @JsonIgnore
    @Override
    public String getAuthority() {
        return roleName;
    }
}
```

### 4. 创建用户pojo

```java
package com.example.springboot_security_jsp.domain;

import com.fasterxml.jackson.annotation.JsonIgnore;
import org.springframework.security.core.GrantedAuthority;
import org.springframework.security.core.userdetails.UserDetails;

import java.util.ArrayList;
import java.util.Collection;
import java.util.List;

/**
 * @author john
 * @date 2020/1/11 - 20:15
 */
public class SysUser implements UserDetails {
    private Integer id;
    private String username;
    private String password;
    private Integer status;
    private List<SysRole> roles = new ArrayList<>();

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public void setPassword(String password) {
        this.password = password;
    }

    public Integer getStatus() {
        return status;
    }

    public void setStatus(Integer status) {
        this.status = status;
    }

    public List<SysRole> getRoles() {
        return roles;
    }

    public void setRoles(List<SysRole> roles) {
        this.roles = roles;
    }

    @JsonIgnore
    @Override
    public Collection<? extends GrantedAuthority> getAuthorities() {
        return roles;
    }

    @Override
    public String getPassword() {
        return password;
    }

    @Override
    public String getUsername() {
        return username;
    }

    @JsonIgnore
    @Override
    public boolean isAccountNonExpired() {
        return true;
    }

    @JsonIgnore
    @Override
    public boolean isAccountNonLocked() {
        return true;
    }

    @JsonIgnore
    @Override
    public boolean isCredentialsNonExpired() {
        return true;
    }

    @JsonIgnore
    @Override
    public boolean isEnabled() {
        return true;
    }
}
```

### 5. 配置`application.yml`

```yml
server:
  port: 8082
spring:
  mvc:
    view:
      suffix: .jsp
      prefix: /pages/
  datasource:
    driver-class-name: com.mysql.jdbc.Driver
    url: jdbc:mysql:///test
    username: root
    password: root
mybatis:
  type-aliases-package: com.example.springboot_security_jsp.domain
  configuration:
    map-underscore-to-camel-case: true
logging:
  level:
    com.demo: debug
```

### 6. 编写`RoleMapper`

```java
package com.example.springboot_security_jsp.mapper;

import com.example.springboot_security_jsp.domain.SysRole;
import org.apache.ibatis.annotations.Select;
import tk.mybatis.mapper.common.Mapper;

import java.util.List;

/**
 * @author john
 * @date 2020/1/11 - 20:20
 */
public interface RoleMapper extends Mapper<SysRole> {
    @Select("select r.id,r.role_name roleName ,r.role_desc roleDesc " +
            "FROM sys_role r,sys_user_role ur " +
            "WHERE r.id=ur.rid AND ur.uid=#{uid}")
    public List<SysRole> findByUid(Integer uid);
}
```

### 7. 编写`UserMapper`

```java
package com.example.springboot_security_jsp.mapper;

import com.example.springboot_security_jsp.domain.SysUser;
import org.apache.ibatis.annotations.Many;
import org.apache.ibatis.annotations.Result;
import org.apache.ibatis.annotations.Results;
import org.apache.ibatis.annotations.Select;
import tk.mybatis.mapper.common.Mapper;

import java.util.List;

/**
 * @author john
 * @date 2020/1/11 - 20:25
 */
public interface UserMapper extends Mapper<SysUser> {
    @Select("select * from sys_user where username=#{username}")
    @Results({
            @Result(id = true, property = "id", column = "id"),
            @Result(property = "roles", column = "id", javaType = List.class,
                    many = @Many(select = "com.example.springboot_security_jsp.mapper.RoleMapper.findByUid"))
    })
    public SysUser findByUsername(String username);
}
```

### 8. 编写`UserService`以及其实现类

```java
package com.example.springboot_security_jsp.service;

import org.springframework.security.core.userdetails.UserDetailsService;

/**
 * @author john
 * @date 2020/1/11 - 20:31
 */
public interface UserService extends UserDetailsService {

}
```

------

```java
package com.example.springboot_security_jsp.service.impl;

import com.example.springboot_security_jsp.mapper.UserMapper;
import com.example.springboot_security_jsp.service.UserService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.security.core.userdetails.UsernameNotFoundException;
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;

/**
 * @author john
 * @date 2020/1/11 - 20:32
 */
@Service
@Transactional
public class UserServiceImpl implements UserService {
    @Autowired
    private UserMapper userMapper;

    @Override
    public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {
        return userMapper.findByUsername(username);
    }
}
```

### 9. `SpringSecurity`配置类

```java
package com.example.springboot_security_jsp.config;

import com.example.springboot_security_jsp.service.UserService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.annotation.authentication.builders.AuthenticationManagerBuilder;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;
import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;

/**
 * @author john
 * @date 2020/1/11 - 19:17
 */
@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Autowired
    private UserService userService;
    @Autowired
    private BCryptPasswordEncoder passwordEncoder;

    @Bean
    public BCryptPasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder();
    }

    // 认证用户的来源(内存或者数据库)
    protected void configure(AuthenticationManagerBuilder auth) throws Exception {
        auth.userDetailsService(userService).passwordEncoder(passwordEncoder);
    }

    //配置springsecurity相关信息
    protected void configure(HttpSecurity http) throws Exception {
        // 释放静态资源，指定资源拦截规则，指定自定义认证页面，指定退出认证配置，csrf配置
        http.authorizeRequests()
                .antMatchers("/login.jsp", "/failer.jsp", "/css/**", "/img/**", "/plugins/**")
                .permitAll()
                .antMatchers("/**").hasAnyRole("USER", "ADMIN")
                .anyRequest().authenticated()
                .and()
                .formLogin()
                .loginPage("/login.jsp")
                .loginProcessingUrl("/login")
                .successForwardUrl("/index.jsp")
                .failureForwardUrl("/failer.jsp")
                .permitAll()
                .and()
                .logout()
                .logoutUrl("/logout")
                .logoutSuccessUrl("/login.jsp")
                .invalidateHttpSession(true)
                .permitAll();
        //禁用csrf
//                .and()
//                .csrf()
//                .disable();
    }

}
```

### 10. 编写启动类

```java
package com.example.springboot_security_jsp;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.security.config.annotation.method.configuration.EnableGlobalMethodSecurity;
import tk.mybatis.spring.annotation.MapperScan;

@SpringBootApplication
@MapperScan("com.example.springboot_security_jsp.mapper")
@EnableGlobalMethodSecurity(securedEnabled = true)
public class SpringbootSecurityJspApplication {

    public static void main(String[] args) {
        SpringApplication.run(SpringbootSecurityJspApplication.class, args);
    }

}
```

### 11. 编写一个控制器用于访问

```java
package com.example.springboot_security_jsp.controller;

import org.springframework.security.access.annotation.Secured;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;

/**
 * @author john
 * @date 2020/1/11 - 19:07
 */
@Controller
@RequestMapping("/product")
public class ProductController {
    @RequestMapping("/findAll")
    @Secured("ROLE_PRODUCT")
    public String hello() {
        return "product-list";
    }
}
```

### 12. 配置异常拦截器

```java
package com.example.springboot_security_jsp.controller.advice;

import org.springframework.security.access.AccessDeniedException;
import org.springframework.web.bind.annotation.ControllerAdvice;
import org.springframework.web.bind.annotation.ExceptionHandler;

/**
 * @author john
 * @date 2020/1/11 - 20:40
 */
@ControllerAdvice
public class HandleControllerException {
    @ExceptionHandler(RuntimeException.class)
    public String exceptionHandler(RuntimeException e) {
        if (e instanceof AccessDeniedException) {
            //如果是权限不足异常，则跳转到权限不足页面！
            return "redirect:/403.jsp";
        }
        //其余的异常都到500页面！
        return "redirect:/500.jsp";
    }
}
```

### 13. 测试

jsp等静态页面资源查看码云代码

SpringBoot官方是不推荐在SpringBoot中使用jsp的，需要导入tomcat插件启动项目，不能再用SpringBoot默认tomcat了

在maven中执行

```
mvn spring-boot:run
```

[![img](/home/jason/learningstuff/spring security/Untitled.assets/1580998-20200112193710358-241776495.png)](https://img2018.cnblogs.com/blog/1580998/202001/1580998-20200112193710358-241776495.png)

打开浏览器访问``

[![img](/home/jason/learningstuff/spring security/Untitled.assets/1580998-20200112193720065-1646104275.png)](https://img2018.cnblogs.com/blog/1580998/202001/1580998-20200112193720065-1646104275.png)

输入用户名`john`密码123

登录成功
[![img](/home/jason/learningstuff/spring security/Untitled.assets/1580998-20200112193727978-521515981.png)](https://img2018.cnblogs.com/blog/1580998/202001/1580998-20200112193727978-521515981.png)

当访问权限不足的页面会显示自定义页面
[![img](/home/jason/learningstuff/spring security/Untitled.assets/1580998-20200112193738834-1770520791.png)](https://img2018.cnblogs.com/blog/1580998/202001/1580998-20200112193738834-1770520791.png)

正常访问其他页面
[![img](/home/jason/learningstuff/spring security/Untitled.assets/1580998-20200112193752822-796522628.png)](https://img2018.cnblogs.com/blog/1580998/202001/1580998-20200112193752822-796522628.png)

### 14. 代码地址

[demo项目](https://gitee.com/an1993/simple-springboot-springsecurity-jsp)

### 15. 知识点备忘

#### 1. Spring Security主要jar包功能介绍

```
Spring Security主要jar包功能介绍
spring-security-core.jar
核心包，任何Spring Security功能都需要此包。
spring-security-web.jar
web工程必备，包含过滤器和相关的Web安全基础结构代码。
spring-security-config.jar
用于解析xml配置文件，用到Spring Security的xml配置文件的就要用到此包。
spring-security-taglibs.jar
Spring Security提供的动态标签库，jsp页面可以用
```

#### 2. Spring Security 常用过滤器介绍

**1. org.springframework.security.web.context.SecurityContextPersistenceFilter**

首当其冲的一个过滤器，作用之重要，自不必多言。
`SecurityContextPersistenceFilter`主要是使用`SecurityContextRepository`在`session`中保存或更新一个`SecurityContext`，并将`SecurityContext`给以后的过滤器使用，来为后续filter建立所需的上下文。
`SecurityContext`中存储了当前用户的认证以及权限信息。
**2. org.springframework.security.web.context.request.async.WebAsyncManagerIntegrationFilter**
此过滤器用于集成`SecurityContext`到`Spring`异步执行机制中的`WebAsyncManager`
**3 . org.springframework.security.web.header.HeaderWriterFilter**
向请求的`Header`中添加相应的信息,可在`http`标签内部使用`security:headers`来控制
**4 . org.springframework.security.web.csrf.CsrfFilter**
`csrf`又称跨域请求伪造，`SpringSecurity`会对所有`post`请求验证是否包含系统生成的`csrf`的`token`信息，
如果不包含，则报错。起到防止`csrf`攻击的效果。
**5. org.springframework.security.web.authentication.logout.LogoutFilter**
匹配 `URL`为`/logout`的请求，实现用户退出,清除认证信息。
**6 . org.springframework.security.web.authentication.UsernamePasswordAuthenticationFilter**
认证操作全靠这个过滤器，默认匹配`URL`为`/login`且必须为`POST`请求。
**7 . org.springframework.security.web.authentication.ui.DefaultLoginPageGeneratingFilter**
如果没有在配置文件中指定认证页面，则由该过滤器生成一个默认认证页面。
**8 . org.springframework.security.web.authentication.ui.DefaultLogoutPageGeneratingFilter**
由此过滤器可以生产一个默认的退出登录页面
**9 . org.springframework.security.web.authentication.www.BasicAuthenticationFilter**
此过滤器会自动解析`HTT`P请求中头部名字为`Authentication`，且以`Basic`开头的头信息。
**10 . org.springframework.security.web.savedrequest.RequestCacheAwareFilter**
通过`HttpSessionRequestCache`内部维护了一个`RequestCache`，用于缓存`HttpServletRequest`
**11 . org.springframework.security.web.servletapi.SecurityContextHolderAwareRequestFilter**
针对`ServletRequest`进行了一次包装，使得`request`具有更加丰富的`API`
**12 . org.springframework.security.web.authentication.AnonymousAuthenticationFilter**
当`SecurityContextHolder`中认证信息为空,则会创建一个匿名用户存入到`SecurityContextHolder`中。
`spring security`为了兼容未登录的访问，也走了一套认证流程，只不过是一个匿名的身份。
**13 . org.springframework.security.web.session.SessionManagementFilter**
`SecurityContextRepository`限制同一用户开启多个会话的数量
**14 . org.springframework.security.web.access.ExceptionTranslationFilter**
异常转换过滤器位于整个`springSecurityFilterChain`的后方，用来转换整个链路中出现的异常
**15 . org.springframework.security.web.access.intercept.FilterSecurityInterceptor**
获取所配置资源访问的授权信息，根据`SecurityContextHolder`中存储的用户信息来决定其是否有权限。

#### 3. csrf处理

##### 1. 禁用csrf,在配置文件编写(不推荐)

[![img](/home/jason/learningstuff/spring security/Untitled.assets/1580998-20200112193813765-1122704889.png)](https://img2018.cnblogs.com/blog/1580998/202001/1580998-20200112193813765-1122704889.png)

##### 2. 在认证页面携带token请求

[![img](/home/jason/learningstuff/spring security/Untitled.assets/1580998-20200112193825756-2115523409.png)](https://img2018.cnblogs.com/blog/1580998/202001/1580998-20200112193825756-2115523409.png)

#### 4. 退出登录

注意：一旦开启了`csrf`防护功能，`logout`处理器便只支持`POST`请求方式了！

```html
<form action="${pageContext.request.contextPath}/logout" method="post">
<security:csrfInput/>
<input type="submit" value="注销">
</form>
```

#### 5. remember me页面

```html
<!-- 注意name和value属性的值不要写错哦 -->
<input type="checkbox" name="remember-me" value="true"> 
```

#### 6. 持久化remember me信息

创建一张表，注意这张表的名称和字段都是固定的，不要修改。

```sql
CREATE TABLE `persistent_logins` (
`username` varchar(64) NOT NULL,
`series` varchar(64) NOT NULL,
`token` varchar(64) NOT NULL,
`last_used` timestamp NOT NULL,
PRIMARY KEY (`series`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

在代码中如下配置

```java
	@Autowired
    private DataSource dataSource;

	// 1. 配置TokenRepository
    @Bean
    public PersistentTokenRepository persistentTokenRepository() {
        JdbcTokenRepositoryImpl tokenRepository = new JdbcTokenRepositoryImpl();
        tokenRepository.setDataSource(dataSource);
        //自动创建上面的表
        tokenRepository.setCreateTableOnStartup(true);
        return tokenRepository;
    }

	@Override
    protected void configure(HttpSecurity http) throws Exception {
        // 表单登录
        http    
                //记住我的配置
                // rememberMe需要的配置包含TokenRepository对象以及token过期时间
                .rememberMe()
                .tokenRepository(persistentTokenRepository())
                .tokenValiditySeconds(60 * 60 * 24)
                .userDetailsService(userDetailsService);
    }
```

#### 7. 在页面中显示当前认证用户名

```jsp
<span class="hidden-xs">
<security:authentication property="principal.username" />
</span>
或者
<span class="hidden-xs">
<security:authentication property="name" />
</span>
```

#### 8. 在页面中控制连接是否显示

```jsp
 					<%-- 管理员和商品管理权限可以--%>
                    <security:authorize access="hasAnyRole('ROLE_PRODUCT','ROLE_ADMIN')">
                        <li id="system-setting"><a
                                href="${pageContext.request.contextPath}/product/findAll">
                            <i class="fa fa-circle-o"></i> 产品管理
                        </a></li>
                    </security:authorize>
                    <%-- 管理员和订单权限可以--%>
                    <security:authorize access="hasAnyRole('ROLE_ORDER','ROLE_ADMIN')">
                        <li id="system-setting"><a
                                href="${pageContext.request.contextPath}/order/findAll">
                            <i class="fa fa-circle-o"></i> 订单管理
                        </a></li>
                    </security:authorize>
```

#### 9. 授权操作

`SpringSecurity`可以通过注解的方式来控制类或者方法的访问权限。

##### 1. securedEnabled

`securedEnabled`是`SpringSecurity`提供的注解

在入口处配置

```java
@SpringBootApplication
@EnableGlobalMethodSecurity(securedEnabled = true)
public class SpringbootSecurityJspApplication {

    public static void main(String[] args) {
        SpringApplication.run(SpringbootSecurityJspApplication.class, args);
    }

}
```

在`controller`处写

```java
@Controller
@RequestMapping("/product")
public class ProductController {
    @Secured({"ROLE_PRODUCT","ROLE_ADMIN"})  //springsecurity内部的权限控制注解开关
    @RequestMapping("/findAll")
    public String findAll(){
        return "product-list";
    }
}
```

##### 2. jsr250注解

在入口处配置

```java
@SpringBootApplication
//表示支持jsr250-api的注解，需要jsr250-api的jar包
@EnableGlobalMethodSecurity(jsr250Enabled = true)
public class SpringbootSecurityJspApplication {

    public static void main(String[] args) {
        SpringApplication.run(SpringbootSecurityJspApplication.class, args);
    }

}
```

在`controller`处写

```java
@Controller
@RequestMapping("/product")
public class ProductController {
   
    @RolesAllowed({"ROLE_PRODUCT", "ROLE_ADMIN"}) //jsr250注解
    @RequestMapping("/findAll")
    public String findAll() {
        return "product-list";
    }
}
```

##### 3. prePostEnabled

在入口处配置

```java
@SpringBootApplication
//表示支持spring表达式注解
@EnableGlobalMethodSecurity(prePostEnabled = true)
public class SpringbootSecurityJspApplication {

    public static void main(String[] args) {
        SpringApplication.run(SpringbootSecurityJspApplication.class, args);
    }

}
```

在`controller`处写（如下两种方式）

```java
@Controller
@RequestMapping("/product")
public class ProductController {
    //SpringSecurity提供的注解
//    @PreAuthorize("hasAnyRole('ROLE_PRODUCT','ROLE_ADMIN')")
    @PreAuthorize("hasAnyAuthority('ROLE_PRODUCT','ROLE_ADMIN')")
    @RequestMapping("/findAll")
    public String findAll(){
        return "product-list";
    }
}
```

以上三种选一种即可

#### 10. 编写异常处理器处理异常

```java
@ControllerAdvice
public class ControllerExceptionAdvice {
    //只有出现AccessDeniedException异常才调转403.jsp页面
    @ExceptionHandler(AccessDeniedException.class)
    public String exceptionAdvice(){
    	return "forward:/403.jsp";
    }
}
```