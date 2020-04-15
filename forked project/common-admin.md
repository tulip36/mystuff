##  后台管理系统

### 1. 功能说明

网址： https://github.com/tulip36/common-admin

后台管理（Springboot+shiro+freemarker+mysql）。拥有基础的菜单管理、用户管理、角色管理等，菜单管理动态生成菜单、权限内容，开发者可以直接拿来使用。项目结构清晰、通俗易懂，是做一个后台管理系统的最佳选择，同时也可以作为任何系统的基础脚手架。

### 2. 将该项目下载下来后，需要改动如下部分才能运行。

- 在pom.xml里，将下面的版本号该为1.5.22。

  ```xml
  	<parent>
  		<groupId>org.springframework.boot</groupId>
  		<artifactId>spring-boot-starter-parent</artifactId>
  		<version>1.5.6.RELEASE</version>
  		<relativePath/> <!-- lookup parent from repository -->
  	</parent>
  
  ```

- 在src/main/resources/config/logback.xml里，将/export前面的/去掉。

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <configuration
          scan="true" scanPeriod="10 seconds">
      <include resource="org/springframework/boot/logging/logback/base.xml"/>
      <appender name="INFO_FILE" class="ch.qos.logback.core.rolling.RollingFileAppender">
          <File>export/Logs/common-admin/info.log</File>
          <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
              <fileNamePattern>export/Logs/common-admin/info-%d{yyyyMMdd}.log.%i</fileNamePattern>
              <timeBasedFileNamingAndTriggeringPolicy class="ch.qos.logback.core.rolling.SizeAndTimeBasedFNATP">
                  <maxFileSize>500MB</maxFileSize>
              </timeBasedFileNamingAndTriggeringPolicy>
              <maxHistory>2</maxHistory>
          </rollingPolicy>
          <layout class="ch.qos.logback.classic.PatternLayout">
              <Pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} [%thread] %-5level %logger{36} -%msg%n
              </Pattern>
          </layout>
      </appender>
  
      <appender name="ERROR_FILE" class="ch.qos.logback.core.rolling.RollingFileAppender">
          <filter class="ch.qos.logback.classic.filter.ThresholdFilter">
              <level>ERROR</level>
          </filter>
          <File>export/Logs/common-admin/error.log</File>
          <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
              <fileNamePattern>/export/Logs/common-admin/error-%d{yyyyMMdd}.log.%i
              </fileNamePattern>
              <timeBasedFileNamingAndTriggeringPolicy class="ch.qos.logback.core.rolling.SizeAndTimeBasedFNATP">
                  <maxFileSize>500MB</maxFileSize>
              </timeBasedFileNamingAndTriggeringPolicy>
              <maxHistory>2</maxHistory>
          </rollingPolicy>
          <layout class="ch.qos.logback.classic.PatternLayout">
              <Pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} [%thread] %-5level %logger{36} -%msg%n
              </Pattern>
          </layout>
      </appender>
      <appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">
          <encoder>
              <pattern>%d{HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n
              </pattern>
          </encoder>
      </appender>
      <!-- 这一句至关重要如果没有，就无法输出sql语句 -->
      <logger name="com.common.system.mapper" level="DEBUG"/>
      <root level="INFO">
          <appender-ref ref="INFO_FILE"/>
          <appender-ref ref="ERROR_FILE"/>
      </root>
  </configuration>
  ```

  ### 3. 登录密码是super, 123456

  ### 4. 在src/main/resource/application.properties里，修改数据源的设置

  ```xml
  spring.datasource.type=com.alibaba.druid.pool.DruidDataSource
  spring.datasource.url=jdbc:mysql://localhost:3306/common_admin?characterEncoding=utf-8
  spring.datasource.username=root
  spring.datasource.password=root
  ```

  