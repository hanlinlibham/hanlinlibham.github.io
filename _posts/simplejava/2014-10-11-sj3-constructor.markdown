---
layout: post
category: "java"
title:  "[SimpleJava]-构造函数"
tags: [simplejava]
---

####1.为什么子类创建的时候会调用父类的构造函数？

{% highlight java %}
class Super {
    String s;
 
    public Super(){
    	System.out.println("Super");
    }
}
 
public class Sub extends Super {
 
    public Sub(){
    	//super(); 也可以显示调用
    	System.out.println("Sub");
    }
 
    public static void main(String[] args){
    	Sub s = new Sub();
    }
}
{% endhighlight %}

并不是创建了父类对象，而是父类有可能要通过构造函数初始化一些字段给子类访问。

####2.常见错误

"Implicit super constructor is undefined for default constructor. Must define an explicit constructor"。

![pic1](http://www.programcreek.com/wp-content/uploads/2013/04/Implicit-super-constructor-is-undefined-for-default-constructor.png)

原因是Super没有定义默认的构造函数。如果一个类显示定义构造函数，默认的就不会被加入。当编译器尝试给Sub加入super()时发现没有就报错了。解决的办法有3个：

* Super加入默认构造函数；

* 删除Super的自定义构造函数；

* 显示添加super(value)到子类的构造函数中；

![pic2](http://www.programcreek.com/wp-content/uploads/2013/04/sub-constructor-with-parameter.png)

####3.有趣的问题：为什么java在有其他构造函数时不再提供默认的？

主要是为了安全和接口[here](http://stackoverflow.com/questions/16046200/why-java-doesnt-provide-default-constructor-if-class-has-parametrized-construc)
