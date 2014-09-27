---
layout: post
category: "java"
title:  "[SimpleJava]-String的不可变性"
tags: [simplejava]
---
### 图说string的不可变
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
### String为什么不可变？
1. String Pool
   字符串池是方法区内的特殊区域，当一个string创建时，如果池中有相同的string，则直接返回引用。
   下面的代码只创建了一个对象，工作图示看图2。如果string不可变，改变其中一个值，另一个string也会改变了，这显然不合适。所以，池的设计要求string不变。
	{% highlight java %}
	String s1 = "abcd";
	String s2 = "abcd";
	{% endhighlight %}
2. 缓存hashcode
	string的hashcode是经常被用到的，不变性可以让hashcode缓存起来，不用每次计算，很高效。
3. 方便使用其他对象
{% highlight java %}
HashSet<String> set = new HashSet<String>();
set.add(new String("a"));
set.add(new String("b"));
set.add(new String("c"));
for(String a: set)
	a.value = "a";
{% endhighlight %}
这个例子中如果string可以改变，将违反set的规则。
4. 安全
	string作为参数被广泛的使用在网络连接，文件操作，反射等方面，如果可变将会出现问题。
5. 线程安全
	不变性使得多线程共享是安全的。
总之，string的不可变性是为了高效和安全。