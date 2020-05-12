###### pom.xml
```xml
<!-- JASYPT: Spring 3.1x Simplified Encryption -->
<dependency>
  <groupId>org.jasypt</groupId>
  <artifactId>jasypt-spring31</artifactId>
  <version>1.9.2</version>
</dependency>
```
###### spring config xml
```xml
<bean id="encryptorConfig" class="org.jasypt.encryption.pbe.config.EnvironmentPBEConfig">
  <property name="algorithm" value="PBEWithMD5AndDES" />
  <property name="password" value="!referenceKey@" />
</bean>

<bean id="encryptor" class="org.jasypt.encryption.pbe.StandardPBEStringEncryptor">
  <property name="config" ref="encryptorConfig" />
</bean>

<bean class="org.jasypt.spring31.properties.EncryptablePropertyPlaceholderConfigurer">
  <constructor-arg ref="encryptor" />
  <property name="locations">
    <list>
      <value>classpath:/properties/application.xml</value>
    </list>
  </property>
</bean>
```
###### application.xml
```xml
<properties>
	<comment>application properties</comment>
	<entry key="constants.session.time">86400</entry>
	<entry key="dataSource.url">jdbc:mysql://127.0.0.1:37737/m8?useUnicode=true&amp;characterEncoding=utf-8&amp;autoReconnect=true&amp;serverTimezone=UTC</entry>
	<entry key="dataSource.username">ENC(encrypted-string)</entry>
	<entry key="dataSource.password">ENC(encrypted-string)</entry>
	<entry key="constants.image.path">D:/git/datai/ibk.ivr.ca/ca/src/main/webapp/resources/report/</entry>
	<entry key="constants.image.server">http://127.0.0.1:37737</entry>
</properties>
```
###### datasource.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
	<bean id="dataSource" class="org.apache.commons.dbcp2.BasicDataSource" destroy-method="close">
        <property name="driverClassName" value="com.mysql.cj.jdbc.Driver"/>
        <property name="url" value="${dataSource.url}"/>
        <property name="username" value="${dataSource.username}"/>
        <property name="password" value="${dataSource.password}"/>
        <property name="initialSize" value="5"/>
        <property name="maxIdle" value="200"/>
        <property name="minIdle" value="100"/>
        <property name="validationQuery" value="SELECT 1"/>
        <property name="testWhileIdle" value="true"/>
        <property name="timeBetweenEvictionRunsMillis" value="25200000"/>
    </bean>
</beans>
```