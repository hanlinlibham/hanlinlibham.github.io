---
layout: post
category: "java"
title:  "[SimpleJava]-java.util.ConcurrentModificationException"
tags: [simplejava]
---
下面的代码会产生ConcurrentModificationException异常。

{% highlight java %}
public static void main(String args[]) {
	List<String> list = new ArrayList<String>();
	list.add("A");
	list.add("B");

	for (String s : list) {
		if (s.equals("B")) {
			list.remove(s);
		}
	}
}
{% endhighlight %}

解决方法1，使用Iterator，2，用CopyOnWriteList代替，因为他对所有可变操作实现了线程安全。

Set、LinkedList都没有这个异常，因为他们不是基于数组实现的。