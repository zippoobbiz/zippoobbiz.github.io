---
title: Design Patterns in JDK
date: 2018-02-21 22:35:27
tags: [Design Pattern]
categories: [Theory, Design Pattern]
---

![design-patterns](https://philsblog.b-cdn.net/images/design-patterns.png "design-patterns")

|Design Pattern|Example in JDK|Description
|:-|:-|:-|
|Singleton|Runtime (hungry)<br/>NumberFormat||
|Factory|Integer.valueOf<br/>CLass.forName|Replace constructor<br/>Method name is more informative than constructor|
|Factory Method|Collection.oterator||
|Abstract Factory|java.sql<br/>UIManager||
|Builder|DocumentBuilder||
|Prototype|Object.clone<br/>Cloneable||
|Adapter|java.io.InputStreamReader(InputStream)<br/>java.io.OutputStreamWriter(OutputStream)||
|Bridge|Handler & Formatter in java.util.logging||
|Composite|javax.swing.JComponent#add||
|Decorator|java.io||
|Facade|||
|Flyweight|String constant pool||
|Proxy|RMI||
|Iterator|Iterator||
|Observer|java.util.Observer, Observable<br/>Listener||
|Mediator|Swing ButtonGroup||
|Template method|||
|Strategy|||
|Chain of Responsibility|ClassLoader<br/>java.util.logging.Logger||
|Command|Runnable<br/>Callable<br/>ThreadPoolExecutor||
|Interpreter|java.util.regex.Pattern||




