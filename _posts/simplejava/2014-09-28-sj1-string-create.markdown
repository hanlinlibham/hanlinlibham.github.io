---
layout: post
category: "java"
title:  "[SimpleJava]-创建String2种方法"
tags: [simplejava]
---
1. 双引号和构造函数
这两种创建方式看下面的代码：
{% highlight java %}
String a = "abcd";
String b = "abcd";
System.out.println(a == b);  // True
System.out.println(a.equals(b)); // True
{% endhighlight %}
a==b是因为两个变量指向的同一个引用。
{% highlight java %}
String c = new String("abcd");
String d = new String("abcd");
System.out.println(c == d);  // False
System.out.println(c.equals(d)); // True
{% endhighlight %}
c！=d是因为它们指向了不同的对象。
![pic1](http://www.programcreek.com/wp-content/uploads/2014/03/constructor-vs-double-quotes-Java-String-New-Page-650x324.png)
2. Run-Time String Interning
intern不知道怎么翻译，意思大概就是运行时确定。看例子：
{% highlight java %}
String c = new String("abcd").intern();
String d = new String("abcd").intern();
System.out.println(c == d);  // True
System.out.println(c.equals(d)); // True
{% endhighlight %}
构造函数的string还在heap中，没法在编译期确定，intern方法的作用就是查看string pool中是否有对应的值，然后把引用指过去，所以cd就true了。
3. 总结
因为构造函数会在heap中多创建一个对象，所有，通常情况下使用""是更好的选择。