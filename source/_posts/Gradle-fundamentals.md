---
title: Gradle fundamentals
date: 2018-05-20 21:12:00
tags: [Tools, Gradle]
categories: [Dev, Gradle]
---

Build
```bash
gradle clean
gradle build
```

Run application
```bash
# add application plugin
apply plugin 'application'

# add main class
mainClassName = 'com.mycompany.Main'

gradle run

```
![gradle](https://philsblog.b-cdn.net/images/gradle.png "gradle")

