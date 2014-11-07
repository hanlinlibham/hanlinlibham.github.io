---
layout: post
category: "java"
title:  "java程序员常犯的10个错误"
tags: [java]
---
#### 1. 数组转换成list

<pre>List<String> list = Arrays.asList(arr);</pre>

这是jdk一个坑爹的敌方，Arrays.asList返回一个ArrayList，但它是Arrays的一个内部静态类，和我们常用的util包里的完全不是一回事。正确的做法：

<pre>ArrayList<String> arrayList = new ArrayList<String>(Arrays.asList(arr));</pre>

#### 2. 检查数组是否存在某个值

<pre>
Set<String> set = new HashSet<String>(Arrays.asList(arr));
return set.contains(targetValue);
</pre>

这代码可以工作，但不需要花费额外时间转换成set。直接使用工具类：或者自己循环也可以。

<pre>Arrays.asList(arr).contains(targetValue);</pre>

#### 3. 在循环内部从list重移除元素

<pre>
for (int i = 0; i < list.size(); i++) {
	list.remove(i);
}
</pre>

当元素被删除时，list的尺寸和index都改变了。当使用index删除多个元素，代码将不能正常工作。

foreach即for的简化写法也是不正确的，会抛出ConcurrentModificationException异常。正确的方法是迭代器：

<pre>
Iterator<String> iter = list.iterator();
while (iter.hasNext()) {
	String s = iter.next();
	if (s.equals("a")) {
		iter.remove();
	}
}
</pre>

#### 4. Hashtable vs HashMap

2者主要的区别就是同步。

#### 5. 使用泛型集合

泛型RawType和无限制通配符容易混淆。例如Set是泛型，Set<?>是通配符。

使用泛型是不安全的，忽略了类型检查。

<pre>
public static void add(List list, Object o){
	list.add(o);
}
public static void main(String[] args){
	List<String> list = new ArrayList<String>();
	add(list, 10);
	String s = list.get(0);
}
</pre>

抛出异常：java.lang.ClassCastException: java.lang.Integer cannot be cast to java.lang.String

#### 6. 访问级别

对属性使用public级别是很烂的设计，尽可能的让访问级别低。

#### 7. ArrayList vs LinkedList

大量add、remove操作而较少遍历操作使用LinkedList。

#### 8. 可变 vs 不可变

不可变对象有很多好处，简单、安全，但单个对象有唯一的值，太多的对象导致gc消耗大。需要平衡使用。

一般，可变对象被使用于避免产生太多的中间对象。一个经典的例子是大字符串连接。如果使用String将会创建非常多的对象，应该使用StringBuilder。

另一个场景使用可变对象很合适。可变对象作为参数传递进方法用来集合多个结果，跳出过多的词法限制。另一个例子是排序和过滤。你可以返回一个新的集合，但这浪费空间。

#### 9. 超类和子类的构造器

![pic1](http://www.programcreek.com/wp-content/uploads/2013/04/Implicit-super-constructor-is-undefined-for-default-constructor.png)

编译错误是因为超类没有定义默认构造器。超类有了自定义构造器，默认的就不会被加入。子类调用默认的编译器尝试插入super()方法但找不到。

#### 10. String “” 还是构造









































