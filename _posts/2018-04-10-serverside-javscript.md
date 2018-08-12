---
author: teymur
comments: true
date: 2019-04-09 00:00:00+00:00
layout: post
slug: rhino
title: Rhino
categories: Tutorial
published: false
tags:
- java
- rhino
---

 
Rhino is a SSJS engine, which is written in Java.

Rhino compiled all java script code to java byte code.

Rhino works in both compiled as well as interpreted mode. 

Spider Monkey is a SSJS engine written in C.
It provides java script support for Mozilla firefox. It contains an interpreter, JIT compiler and garbage collector.  The Spider Monkey to be used in the Java script shel

The V8 Java script engine is an open source Java script engine developed by Google for Chrome browser. The first of engine was released on 2008. V8 complies Java script to native machine code before executing it, instead of more traditional techniques such as interpreting byte code or compiling the whole program to machine code and executing it from a file system.


Jscript is Microsoft’s dialect of the EMCA script standard that is used in IE browsers. Jscript is implemented as an Active scripting engine. Jscript was first supported in IE 3.0, now the recent version is Jscript 9.0 in Internet explorer 9. 


SSJS Frameworks

SSJS Frameworks provide an API to work on the server side java scripts. They will get executed inside the SSJS Engines. Some of the popular frameworks available in the market are Node JS based on V8, Ringo JS based on Common JS, Narwhal based on Common JS, ASP based on JScript, Wakanda based on Squirrel fish.

https://dzone.com/articles/evolution-server-side-java

Usage of SSJS in some of the popular project / products

Product name | SSJS Engine | Server platform
--- | --- | ---
Node JS | V8 | Standalone
Alfresco | Rhino | Java servlet container / standalone
 ASP | Jscript | IIS
 Mango DB | V8 | 10gen
 Jaxer | Spider Monkey | Standalone
 Couch DB | Spider Monkey | Standalone



 Invoking Class#forName() will execute all static initializers.


 1 : if you are interested only in the static block of the class , the loading the class only would do , and would execute static blocks then all you need is:

Class.forName("Somthing");

2 : if you are interested in loading the class , execute its static blocks and also want to access its its non static part , then you need an instance and then you need:

Class.forName("Somthing").newInstance();


// import the java sql packages
importPackage( java.sql );

E4X (ECMAScript for XML) is an extension of JavaScript which provides direct support for XML, greatly simplifying the process of consuming XML via JavaScript. 


java.io. - ?

https://developer.mozilla.org/en-US/docs/Archive/Web/Server-Side_JavaScript/Walkthrough


Apache Ant

Binary and source code 

Set environmental variables: JAVA_HOME


-classpath classpath
Set the user class path, overriding the user class path in the CLASSPATH environment variable

CLASSPATH tells the compiler and the class loader where to look for the .class files it needs.

Sourcepath is something I don't use so much. I believe it's optional, because usually the current directory is the sourcepath. CLASSPATH is not.


classpath is searched for class (.class) files
sourcepath is searched for source (.java) files (.a.k.a class or interface definitions)
However, if sourcepath is NOT specified, the classpath is searched for both class files AND source files.


So the buildfile contains targets

```
    <target name="clean" description="Delete all generated files">
        <delete dir="classes"/>
        <delete file="MyTasks.jar"/>
    </target>
```

```
<property name="src.dir" value="src"/>

<target name="clean" description="Delete all generated files">
        <delete dir="${classes.dir}" failonerror="false"/>
        <delete file="${ant.project.name}.jar"/>
    </target>

```
Write the Task

The basic procedure for creating a custom task includes:

Creating a Java class that subclasses org.apache.tools.ant.Task and overrides the execute() method.
Packaging your class file(s) into a jar file.
In a standard Ant build.xml file, registering your custom task by using the standard taskdef task.


```
public class HelloWorld {
    public void execute() {
        System.out.println("Hello World");
    }
}
```

```
<target name="use" description="Use the Task" depends="jar">
        <taskdef name="helloworld" classname="HelloWorld" classpath="${ant.project.name}.jar"/>
        <helloworld/>
    </target>
```


build.xml
```
<?xml version = "1.0"?>
<project name = "Hello World Project" default = "info">
   <property file = "build.properties"/>
   
   <target name = "info">
      <echo>Apache Ant version is ${ant.version} - You are at ${sitename} </echo>
   </target>
</project>
```
build.properties
```
sitename = www.tutorialspoint.com
buildversion = 3.3.2
```