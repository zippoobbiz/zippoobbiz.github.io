---
title: Spring Framework Intro
date: 2017-09-02 09:22:08
tags: [Spring]
categories: [Framework, Spring]
---

![spring](/spring.png "spring")

## BeanFactory
It's a simple container which provides Dependency Injection. It's defined in org.springframework.beans.factory.BeanFactor.
There are many instances of BeanFactory, one of the most used is XmlBeanFactory, it reads from a XML file to config the meta data.

## ApplicationContext

It's similar to BeanFactory, it loads the defination of the beans from the config file. It's defined in org.springframework.context.ApplicationContext interface.

ApplicationContext contains all BeanFactor's functions. Normally, ApplicationContext is recommended. BeanFactory will be used in light-weight apps.
* FileSystemXmlApplicationContext
It reads from XML file, and the path of the file is needed
* ClassPathXmlApplicationContext
The path of xml file should be included in the CLASSPATH
* WebXmlApplicationContext


```Java
# ClassPathXmlApplicationContext
	public static void main(String[] args) {
      ApplicationContext context = 
             new ClassPathXmlApplicationContext("Beans.xml");
      HelloWorld obj = (HelloWorld) context.getBean("helloWorld");
      obj.getMessage();
   }

# FileSystemXmlApplicationContext
    public static void main(String[] args) {
      ApplicationContext context = new FileSystemXmlApplicationContext
            ("C:/Users/ZARA/workspace/HelloSpring/src/Beans.xml");
      HelloWorld obj = (HelloWorld) context.getBean("helloWorld");
      obj.getMessage();
   }
```
