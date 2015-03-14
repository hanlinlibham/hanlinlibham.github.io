---
layout: post
category: "java"
title:  "[SimpleJava]-数组转换成list"
tags: [simplejava]
---
#### 1.

{% highlight java %}
ArrayList<Element> arrayList = new ArrayList<Element>(Arrays.asList(array));
{% endhighlight %}

ArrayList的JavaDoc描述：ArrayList(Collection < ? extends E > c) : Constructs a list containing the elements of the specified collection, in the order they are returned by the collection's iterator. 构造函数做了2件事：

*  转换collection c 为一个数组；
*  copy数组到内部的一个elementData中；

源码：

{% highlight java %}
public ArrayList(Collection<? extends E> c) {
       elementData = c.toArray();
       size = elementData.length;
 
       if (elementData.getClass() != Object[].class)
             elementData = Arrays.copyOf(elementData, size, Object[].class);
}
{% endhighlight %}

#### 2.
·List<Element> list = Arrays.asList(array);·

这种方式有个问题，实际上asList返回的是Arrays的一个内部类Arraylist，所以当list.add(new Element(4));将会报一个类型转换错误。

#### 3.
这种方式效率比第一种要高一些。
{% highlight java %}
Element[] array = {new Element(1), new Element(2)};
List<element> list = new ArrayList<element>(array.length);
Collections.addAll(list, array);
{% endhighlight %}
