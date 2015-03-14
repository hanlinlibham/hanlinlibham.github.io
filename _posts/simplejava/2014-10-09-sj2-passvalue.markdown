---
layout: post
category: "java"
title:  "[SimpleJava]-值传参"
tags: [simplejava]
---
>java是值传参的。

####1.定义

值传递：复制内存中实参的值进行传递；

引用传递：复制实参的地址进行传递；

Java is always pass-by-value. Primitive data types and object reference are just values.

####2.基本类型
因为是值传递，下面的代码不能进行swap：
{% highlight java %}
swap(Type arg1, Type arg2) {
    Type temp = arg1;
    arg1 = arg2;
    arg2 = temp;
}
{% endhighlight %}

####3.对象类型
java通过引用操作对象，所有对象变量都是引用。但java是值传递的，不能通过引用传递方法参数，问题是对象为什么会改变？

![pic1](http://www.programcreek.com/wp-content/uploads/2011/08/java-pass-by-value1.jpg)
{% highlight java %}
class Apple {
	public String color="red";
}
 
public class Main {
	public static void main(String[] args) {
		Apple apple = new Apple();
		System.out.println(apple.color);
 
		changeApple(apple);
		System.out.println(apple.color);
	}
 
	public static void changeApple(Apple apple){
		apple.color = "green";
	}
}
{% endhighlight %}
传递的是地址值的拷贝，而地址指向的是同一个对象，所以，对象值改变了。
![pic1](http://www.programcreek.com/wp-content/uploads/2011/08/copied-reference.jpg)

