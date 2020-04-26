---
title: Another neat tool -- automate your build process using Java and Ant
date: 2016-12-03 16:47:06
tags: [Tools, ANT]
categories: [Dev, ANT]
---

> Apache Ant is a Java library and command-line tool whose mission is to drive processes described in build files as targets and extension points dependent upon each other. The main known usage of Ant is the build of Java applications. — ant.apache.org
> 
> ANT is similar to **Make**, the most immediately noticeable difference between **Ant** and **Make** is that **Ant** uses XML to describe the build process and its dependencies, whereas *Make* uses Makefile format. By default the XML file is named build.xml. Ant is an Apache project. It is open source software, and is released under the Apache License. — Wikipedia

A build file looks like this:

```xml
<project>
    <target name="clean">
        <delete dir="build"/>
    </target>
    <target name="compile">
        <mkdir dir="build/classes"/>
        <javac srcdir="src" destdir="build/classes"/>
    </target>
    <target name="jar">
        <mkdir dir="build/jar"/>
        <jar destfile="build/jar/HelloWorld.jar" basedir="build/classes">
            <manifest>
                <attribute name="Main-Class" value="oata.HelloWorld"/>
            </manifest>
        </jar>
    </target>
    <target name="run">
        <java jar="build/jar/HelloWorld.jar" fork="true"/>
    </target>
</project>
```

Now compile, package and run the application via

```
ant compile
ant jar
ant run
```
or shorter with
```
ant compile jar run
```
We can build the same project with pure java command
```
md build\classes
javac
    -sourcepath src
    -d build\classes
    src\oata\HelloWorld.java
echo Main-Class: oata.HelloWorld>mf
md build\jar
jar cfm
    build\jar\HelloWorld.jar
    mf
    -C build\classes
    .
java -jar build\jar\HelloWorld.jar
```
Enhance the build file
```xml
<project name="HelloWorld" basedir="." default="main">
    <property name="src.dir"     value="src"/>
    <property name="build.dir"   value="build"/>
    <property name="classes.dir" value="${build.dir}/classes"/>
    <property name="jar.dir"     value="${build.dir}/jar"/>
    <property name="main-class"  value="oata.HelloWorld"/>
    <target name="clean">
        <delete dir="${build.dir}"/>
    </target>
    <target name="compile">
        <mkdir dir="${classes.dir}"/>
        <javac srcdir="${src.dir}" destdir="${classes.dir}"/>
    </target>
    <target name="jar" depends="compile">
        <mkdir dir="${jar.dir}"/>
        <jar destfile="${jar.dir}/${ant.project.name}.jar" basedir="${classes.dir}">
            <manifest>
                <attribute name="Main-Class" value="${main-class}"/>
            </manifest>
        </jar>
    </target>
    <target name="run" depends="jar">
        <java jar="${jar.dir}/${ant.project.name}.jar" fork="true"/>
    </target>
    <target name="clean-build" depends="clean,jar"/>
    <target name="main" depends="clean,run"/>
</project>
```
just do an **ant** and you will get
```
Buildfile: build.xml
clean:
compile:
    [mkdir] Created dir: C:\...\build\classes
    [javac] Compiling 1 source file to C:\...\build\classes
jar:
    [mkdir] Created dir: C:\...\build\jar
      [jar] Building jar: C:\...\build\jar\HelloWorld.jar
run:
     [java] Hello World
main:
BUILD SUCCESSFUL
```

![apacheant](https://philsblog.b-cdn.net/images/apacheant.png "apacheant")