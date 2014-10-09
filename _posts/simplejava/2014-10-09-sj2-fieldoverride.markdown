---
layout: post
category: "java"
title:  "[SimpleJava]-属性是否能重写"
tags: [simplejava]
---

{% highlight java %}
class Super {
	String s = "Super";
}
 
class Sub extends Super {
	String s = "Sub";
}
 
public class FieldOverriding {
	public static void main(String[] args) {
		Sub c1 = new Sub();
		System.out.println(c1.s);
 
		Super c2 = new Sub();
		System.out.println(c2.s);
	}
}
{% endhighlight %}

输出是sub、super。为什么第二个输出是super？

成员变量不能被重写。子类定义同名属性是一个新的属性，父类的属性被隐藏。

如果要访问隐藏属性：System.out.println(((Super)c1).s)。