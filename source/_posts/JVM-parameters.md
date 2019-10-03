---
title: JVM parameters
date: 2017-06-15 23:35:19
tags: [Java, jvm]
categories: [Language, Java]
---

![jvm](https://philsblog.b-cdn.net/images/jvm.png "jvm")

|参数名称|含义|默认值||
|:-|:-|:-|:-|
|-Xms|初始堆大小|物理内存的1/64(<1GB)|默认(MinHeapFreeRatio参数可以调整)空余堆内存小于40%时，JVM就会增大堆直到-Xmx的最大限制.|
|-Xmx|最大堆大小|物理内存的1/4(<1GB)|默认(MaxHeapFreeRatio参数可以调整)空余堆内存大于70%时，JVM会减少堆直到 -Xms的最小限制|
|-Xmn|年轻代大小(1.4or lator)| |注意：此处的大小是（eden+ 2 survivor space).与jmap -heap中显示的New gen是不同的。<br/>整个堆大小=年轻代大小 + 年老代大小 + 持久代大小. <br/>增大年轻代后,将会减小年老代大小.此值对系统性能影响较大,Sun官方推荐配置为整个堆的3/8|
|-XX:NewSize|设置年轻代大小(for 1.3/1.4)| | |
|-XX:MaxNewSize|年轻代最大值(for 1.3/1.4)| | |
|-XX:PermSize|设置持久代(perm gen)初始值|物理内存的1/64| |
|-XX:MaxPermSize|设置持久代最大值|物理内存的1/4| |
|-Xss|每个线程的堆栈大小| |JDK5.0以后每个线程堆栈大小为1M,以前每个线程堆栈大小为256K.更具应用的线程所需内存大小进行 调整.在相同物理内存下,减小这个值能生成更多的线程.但是操作系统对一个进程内的线程数还是有限制的,不能无限生成,经验值在3000~5000左右 一般小的应用， 如果栈不是很深， 应该是128k够用的 大的应用建议使用256k。这个选项对性能影响比较大，需要严格的测试。（校长） <br/>和threadstacksize选项解释很类似,官方文档似乎没有解释,在论坛中有这样一句话:"-Xss is translated in a VM flag named ThreadStackSize” 一般设置这个值就可以了。|
