---
title: Spring Mybatis Query 결과를 보기 좋게 정렬해보자
date: 2019-08-31 19:28:10
categories:
    - Spring
---
mybatis로 나오는 spring 쿼리를 보기 좋게 포매팅 해보자.

log4j : 속도, 로그 래벨, 멀티스레드 안정성을 고려한 로딩 라이브러리

slf4j : log4j와 같은 로깅 라이브러리의 인터페이스 역할

logback : log4j의 강화판이라고 보면 될듯

log4j -> slf4j -> logback 순서대로 적용된다.

개념은 https://goddaehee.tistory.com/45 사이트에 잘 정리해두셨다.

- **pom.xml**

```xml
		<!-- log4jdbc-remix -->
		<dependency>
			<groupId>org.lazyluke</groupId>
			<artifactId>log4jdbc-remix</artifactId>
			<version>0.2.7</version>
		</dependency>

		<!-- logback -->
		<dependency>
			<groupId>org.slf4j</groupId>
			<artifactId>jcl-over-slf4j</artifactId>
			<version>1.7.13</version>
		</dependency>
		<dependency>
			<groupId>org.slf4j</groupId>
			<artifactId>log4j-over-slf4j</artifactId>
			<version>1.7.13</version>
		</dependency>
		<dependency>
			<groupId>ch.qos.logback</groupId>
			<artifactId>logback-core</artifactId>
			<version>1.1.3</version>
		</dependency>
		<dependency>
			<groupId>ch.qos.logback</groupId>
			<artifactId>logback-classic</artifactId>
			<version>1.1.3</version>
		</dependency>
```


- **context-datasource.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>

<beans xmlns="http://www.springframework.org/schema/beans" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:aop="http://www.springframework.org/schema/aop" xmlns:tx="http://www.springframework.org/schema/tx" xmlns:context="http://www.springframework.org/schema/context" xmlns:jee="http://www.springframework.org/schema/jee" xsi:schemaLocation="
		http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-3.2.xsd
		http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop-3.2.xsd
		http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-3.2.xsd
		http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx-3.2.xsd
		http://www.springframework.org/schema/jee http://www.springframework.org/schema/jee/spring-jee-3.2.xsd">

    <bean id="dataSourceSpied" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
        <property name="driverClassName" value="net.sf.log4jdbc.sql.jdbcapi.DriverSpy"></property>
        <property name="url" value="jdbc:oracle:thin:@url:port:SID"></property>
        <property name="username" value=""></property>
        <property name="password" value=""></property>
    </bean>

    <bean id="dataSource" class="net.sf.log4jdbc.Log4jdbcProxyDataSource">
        <constructor-arg ref="dataSourceSpied" />
        <property name="logFormatter">
            <bean class="net.sf.log4jdbc.tools.Log4JdbcCustomFormatter">
                <property name="loggingType" value="MULTI_LINE" />
                <property name="sqlPrefix" value="SQL : " />
            </bean>
        </property>
    </bean>

    <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
        <property name="dataSource" ref="dataSource" />
        <property name="mapperLocations">
            <list>
                <value>classpath:/config/sql/*.xml</value>
                <value>classpath:/config/sql/*/*.xml</value>
                <value>classpath:/config/sql/*/*/*.xml</value>
                <value>classpath:/config/sql/*/*/*/*.xml</value>
            </list>
        </property>
        <property name="configLocation" value="classpath:/config/mybatis/mybatis-config.xml" />
    </bean>
    
    ...
</beans>
```

- **src/main/resources/logback.xml**

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<configuration>
    <appender name="console" class="ch.qos.logback.core.ConsoleAppender">
        <encoder>
            <pattern>%d{HH:mm:ss} %-5level - %msg%n</pattern>
        </encoder>
    </appender>

    <appender name="file_log" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <file>/app/log/ssp_api.log</file>
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <fileNamePattern>/app/log/ssp_api.%d{yyyy-MM-dd}.%i.log</fileNamePattern>
            <timeBasedFileNamingAndTriggeringPolicy class="ch.qos.logback.core.rolling.SizeAndTimeBasedFNATP">
                <!-- or whenever the file size reaches 100MB -->
                <maxFileSize>100MB</maxFileSize>
            </timeBasedFileNamingAndTriggeringPolicy>
            <maxHistory>30</maxHistory>
        </rollingPolicy>
        <encoder class="ch.qos.logback.classic.encoder.PatternLayoutEncoder">
            <pattern>%d{HH:mm:ss.SSS} {%thread} %-5level %logger{32} - %msg%n</pattern>
        </encoder>
    </appender>

    <!-- <logger name="org.springframework" level="debug"/> <logger name="org.apache.http.wire" level="error" /> <logger name="org.apache.http.client" level="error" /> -->

    <logger name="org.springframework" level="info" />
    <logger name="org.mybatis.spring" level="info" />

    <logger name="jdbc"                level="OFF" />
    <logger name="jdbc.sqlonly"        level="INFO" />  <!-- 파라미터를 셋팅해서 출력-->
    <logger name="jdbc.resultsettable" level="INFO" />  <!-- 결과값을 보여줌-->
    <logger name="jdbc.sqltiming"      level="INFO" />
    <logger name="log4jdbc.debug"      level="INFO" />
    
    <root level="debug">
        <appender-ref ref="console" />
        <appender-ref ref="file_log" />
    </root>
</configuration>

```



- **src/main/resources/log4jdbc.log4j2.properties**


```xml
log4jdbc.spylogdelegator.name=net.sf.log4jdbc.log.slf4j.Slf4jSpyLogDelegator
log4jdbc.dump.sql.maxlinelength=0

```


## Reference

https://addio3305.tistory.com/66

https://goddaehee.tistory.com/45
