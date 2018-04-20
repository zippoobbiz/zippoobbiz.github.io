---
title: Java Currency
date: 2017-01-27 20:31:02
tags: [Java]
categories: [Language, Java]
---


# Use Thread

{% qnimg java_multithreading.png %}

There are three ways of using Thread:

1. Implementes Runnable interface
2. Implementes Callable interface
3. Extends Thread class

Implemeting **Runnable** and **Callable** does not create a new real thead, it only creates a new task and will be invoked by Thread. So i.e. Task is Thread driven.

## Implement Runnable interface

Implement run() method and called by start() from a thread

```java
public class MyRunnable implements Runnable {
    public void run() {
        // ...
    }
    public static void main(String[] args) {
        MyRunnable instance = new MyRunnable();
        Tread thread = new Thread(instance);
        thread.start();
    }
}
```

## Implement Callable interface

Implementing call() method will have return value, the value will be encapsulated in FutureTask

```java
public class MyCallable implements Callable<Integer> {
    public Integer call() {
        // ...
    }
    public static void main(String[]  args) {
        MyCallable mc = new MyCallable();
        FutureTask<Integer> ft = new FutureTask<>(mc);
        Thread thread = new Thread(ft);
        thread.start();
        System.out.println(ft.get());
    }
}
```

## Extend Thread class

Implement run() methond and call start by thread
```java
public class MyThread extends Thread {
    public void run() {
        // ...
    }
    public static void main(String[] args) {
        MyThread mt = new MyThread();
        mt.start();
    }
}
```

# Implementing Interface VS Extending Thread Class

Implementing interface is better, because:
1. Java doesn't support multi-extend, so if a class extends Thread, then it cannot extend other classes.
2. Extending Thread has too much overhead

# Thread mechanism

Thread.sleep(millisec) will put current thread to sleep. Can use TimeUnit.TILLISECONDS.sleep(millisec) instead.

sleep() will through interruptedException. Exception cannot cross threads to main(), so it has to be handled in the local thread.

```java
public void run() {
    try {
        // ...
        Thread.sleep(1000);
        // ...
    } catch (InterruptedException e) {
        System.err.println(e);
    }
}
```

Thread.yield() means the current thead has finished its job, it can hand over to other threads.

Calling join() from another thread would cause the suspension of the current thread, until the target thread finish.

deamon thread is the Program Runtime thread service in the background. 

Use setDaemon() to put a thread in the background.

# Kill a thread

## Stop

A thread can be stop by the following:

1. Call Thread.sleep() method
2. Call wait() to suspend thread untill notify() or notifyAll() is called, Or the signal() signalAll() in java.util.concurrent
3. Until some I/O finish
4. Try to call the sync control method on an object, cannot use object lock, since the thread has got the lock.

## Interrupt






















