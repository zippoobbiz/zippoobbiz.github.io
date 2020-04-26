---
title: Hibernate Configuration
date: 2017-02-18 00:07:41
tags: [Configuration, Hibernate, JPA]
categories: [Dev, Hibernate]
---
![hibernate](https://philsblog.b-cdn.net/images/hibernate.jpeg "hibernate")
> Hibernate ORM (Hibernate in short) is an object-relational mapping tool for the Java programming language. It provides a framework for mapping an object-oriented domain model to a relational database. Hibernate handles object-relational impedance mismatch problems by replacing direct, persistent database accesses with high-level object handling functions.

Diagram
![hibernate](https://philsblog.b-cdn.net/images/hibernate_architecture.jpg "hibernate")

SessionFactory
Session
Transaction
Query
Criteria

## Dependency
|Library|Description|
|:-|:-|
|dom4j|Xml Parsing|
|Xalan|XSLT processing|
|Xerces|The Xerces Java Parser|
|cglib|Java Code Generator|
|log4j|Logging|
|Commons|logger, email|
|SLF4J|logging abstract|

## Properties
|Name|Description|
|:-|:-|
|hibernate.dialet|Specify the SQL language|
|hibernate.connection.driver_class|JDBC driver|
|hibernate.connection.url|DB instance JDBC URL|
|hibernate.connection.username|DB username|
|hibernate.connection.password|DB password|
|hibernate.connection.pool_size|The size of the connection pool|
|hibernate.connection.autocommit|Allow JDBC to autocommit|
If use JNDI
|Name|Description|
|:-|:-|
|hibernate.connection.datasource|JNDI name in your server env|
|hibernate.jndi.class|InitialContext Class|
|hibernate.jndi.<JNDIpropertyname>|Java properties in InitialContext|
|hibernate.jndi.url|JNDI URL|

# A sample of hibernate.cfg.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE hibernate-configuration SYSTEM 
"http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">

<hibernate-configuration>
   <session-factory>
   <property name="hibernate.dialect">
      org.hibernate.dialect.MySQLDialect
   </property>
   <property name="hibernate.connection.driver_class">
      com.mysql.jdbc.Driver
   </property>

   <!-- Assume test is the database name -->
   <property name="hibernate.connection.url">
      jdbc:mysql://localhost/test
   </property>
   <property name="hibernate.connection.username">
      root
   </property>
   <property name="hibernate.connection.password">
      root123
   </property>

   <!-- List of XML mapping files -->
   <mapping resource="Employee.hbm.xml"/>

</session-factory>
</hibernate-configuration>
```
