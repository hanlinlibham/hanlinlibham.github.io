---
layout: post
category: "java"
title:  "[SimpleJava]-String的不可变性"
tags: [simplejava]
---
1. 声明一个String
{% highlight java %}
String s = "abcd";
{% endhighlight %}
![pic1](http://www.programcreek.com/wp-content/uploads/2009/02/String-Immutability-1.jpeg)
2. 赋值
{% highlight java %}
String s2 = s;
{% endhighlight %}
![pic1](http://www.programcreek.com/wp-content/uploads/2009/02/String-Immutability-2.jpeg) 
把s赋值给s2，并没有创建新对象。
3. 连接
{% highlight java %}
s = s.comcat("ef");
{% endhighlight %}
![pic1](http://www.programcreek.com/wp-content/uploads/2009/02/string-immutability-650x279.jpeg) 
连接操作，并没有改变原来s的值，而是创建了新对象，这就是string的不可变性。
一旦string被创建就不会改变了，string的api都不会修改自身，而是创建新对象。如果想使用可变的string，使用StringBuilder。