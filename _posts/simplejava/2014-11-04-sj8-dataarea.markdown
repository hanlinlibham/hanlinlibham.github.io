---
layout: post
category: "java"
title:  "[SimpleJava]-JVM运行时数据区"
tags: [simplejava]
---
java规范中描述的数据区如下：

![pic1](http://www.programcreek.com/wp-content/uploads/2013/04/JVM-runtime-data-area.jpg)

#### 1. 每个独立线程的数据区（非共享）

包括pc寄存器，栈、本地方法栈。新线程创建时他们都会创建。

pc寄存器用来控制每个线程的执行。本地方法栈提供本地方法的支持。

栈由帧构成，当一个方法调用时一个帧压入，一个帧包括如下图：

![pic1](http://www.programcreek.com/wp-content/uploads/2013/04/JVM-Stack.png)

#### 2. 所有线程共享的数据区

包括堆、方法区。

堆：创建对象，gc工作的地方。

方法区：存储运行时常量池、字段、方法数据、方法、构造函数代码。