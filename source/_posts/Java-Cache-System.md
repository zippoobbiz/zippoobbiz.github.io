---
title: Java Cache System
date: 2016-10-13 16:24:59
tags: [Java, cache]
categories: [Dev, Java]
---

> JCS is a distributed caching system written in Java. It is intended to speed up applications by providing a means to manage cached data of various dynamic natures. Like any caching system, JCS is most useful for high read, low put applications. Latency times drop sharply and bottlenecks move away from the database in an effectively cached system.

JCS 1.3 was the first official version. JCS 1.3 working on JDK 1.3+. JCS 2.0 working on JDK 1.6 and above. JCS 1.3 is stable, however it requires a lower version of JDK.

## JCS structure

![Alt text](http://og2api1gp.bkt.clouddn.com/static/images/jcs.jpg "Optional title")

There are following jar files needed:

* commons-collections-2.1.1.jar
* commons-lang.2.3.jar
* commons-logging-1.0.4.jar
* concurrent-1.3.2.jar
* jcs-1.3.jar
* slf4j-api.jar

It implements **Serializable** interface

```java
public class UserInfo implements Serializable{  
    private String username;  
    private String domain;  
  
    public UserInfo(String name){  
      this.username = name;  
    }  
  
    public UserInfo(String name,String domain){  
      this.username= name;  
      this.domain =domain;  
    }  
 }
 ```

 Define Cache Class

 ```java
 public class UserManager{  
    private JCS jcscache;  
    private final String NAME_SPACE="userinfo";  
       
    private static class UserManagerContainer{  
        private static UserManager instance = new UserManager();   
    }  
  
    public static UserManager getInstance(){  
        return UserManagerContainer.instance  
    }  
  
    private UserManager(){  
        try{             
  
            jcscache= JCS.getInstance(NAME_SPACE);  
  
           }  
           catch(CacheException e){  
           }  
    }  
  
    public UserInfo get(String key){  
        return (UserInfo) jcscache.get(key);  
    }  
  
    pubilc void put(String key,UserInfo info,boolean isoverride){  
        try{  
            if(isoverride){  
               jcscache.put(key,info);  
            }  
            else{  
               jcscache.putSafe(key,info);  
            }  
          }  
          catch(CacheException e){  
  
          }  
    }  
}
```

JCS describe its functionality by configuration file, it’s easy to implement, all you need is change the values in configuration file.
Configuration file: *cache.ccf*

```
jcs.default=DC  
jcs.defaultcacheattributes=org.engine.CompositeCacheAttributes  
jcs.defaultcacheattributes.MaxObjects=500000  
jcs.defaultcacheattributes.MemoryCacheName=org.apache.jcs.engine.memory.lru.LRUMemoryCache  
jcs.defaultcacheattributes.UseMemoryShrinker=true  
jcs.defaultcacheattributes.MaxMemoryIdleTimeSeconds=1200  
jcs.defaultcacheattributes.ShrinkerIntervalSeconds=30  
jcs.defaultcacheattributes.MaxSpoolPerRun=500  
jcs.default.elementattributes=org.apache.jcs.engine.ElementAttributes  
jcs.default.elementattributes.IsEternal=false  
jcs.auxiliary.DC=org.apache.jcs.auxiliary.disk.indexed.IndexedDiskCacheFactory  
jcs.auxiliary.DC.attributes=org.apache.jcs.auxiliary.disk.indexed.IndexedDiskCacheAttribute  
jcs.auxiliary.DC.attributes.DiskPatch=d:/memory
```