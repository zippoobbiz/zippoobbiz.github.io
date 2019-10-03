---
title: Spring Bean
date: 2017-09-04 11:15:45
tags: [Spring]
categories: [Framework, Spring]
---

![spring](/spring.png "spring")

## Bean attributes

|Attribute|Description|
|:-|:-|
|class|Necessary, define the class used to create the bean|
|name|unique name identifier, you can use "id" or "name" in XML|
|scope|Define the scope of bean|
|constructor-arg|DI|
|properties|DI|
|autowiring mode|DI|
|lazy-initialization mode|Delay the init until the first use|
|initialization|Define the method that initialize bean|
|destruction|Define the method that destruction bean|

## Spring config meta data
There are three ways of Spring container configuration
* Base on XML file
* Base on annotation
* Base on Java

An example of Spring XML config file
```xml
<?xml version="1.0" encoding="UTF-8"?>

<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
    http://www.springframework.org/schema/beans/spring-beans-3.0.xsd">

   <!-- A simple bean definition -->
   <bean id="..." class="...">
       <!-- collaborators and configuration for this bean go here -->
   </bean>

   <!-- A bean definition with lazy init set on -->
   <bean id="..." class="..." lazy-init="true">
       <!-- collaborators and configuration for this bean go here -->
   </bean>

   <!-- A bean definition with initialization method -->
   <bean id="..." class="..." init-method="...">
       <!-- collaborators and configuration for this bean go here -->
   </bean>

   <!-- A bean definition with destruction method -->
   <bean id="..." class="..." destroy-method="...">
       <!-- collaborators and configuration for this bean go here -->
   </bean>

   <!-- more bean definitions go here -->

</beans>
```

## Bean scope
The scope of bean must be defined. The default scope is singleton

|Scope|Description|
|:-|:-|
|singleton|This scopes the bean definition to a single instance per Spring IoC container (default).|
|prototype|This scopes a single bean definition to have any number of object instances.|
|request|This scopes a bean definition to an HTTP request. Only valid in the context of a web-aware Spring ApplicationContext.|
|session|This scopes a bean definition to an HTTP session. Only valid in the context of a web-aware Spring ApplicationContext.|
|global-session|This scopes a bean definition to a global HTTP session. Only valid in the context of a web-aware Spring ApplicationContext.|

## Bean lifecycle

