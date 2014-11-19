---
layout: post
category: "java"
title:  "java反射"
tags: [java]
---
#### 1. 什么是反射

反射是程序可以改变运行时对象的结构和行为的能力。自省（introspection）是反射的一个子集。有些语言支持自省，不支持反射，如c++。
![p1](http://www.programcreek.com/wp-content/uploads/2013/09/reflection-introspection-650x222.png)

下面是一个自省的例子，检查对象类型：
<pre>
if(obj instanceof Dog){
	Dog d = (Dog)obj;
	d.bark();
}
</pre>
反射的例子：
<pre>
Class<?> c = Class.forName("classpath.and.classname");
Object dog = c.newInstance();
Method m = c.getDeclaredMethod("bark", new Class<?>[0]);
m.invoke(dog);
</pre>

#### 2. 为什么需要反射

反射可以在运行时：

* 检查对象类
* 构造对象
* 检查字段和方法
* 执行类的方法
* 改变构造器、方法、属性的可访问性。

反射经常使用在框架中。如Junit的@Test标注，spring中，通过反射在配置文件中创建类。servlet的配置也一样。

#### 3. 怎样使用反射

获取对象名
<pre>
import java.lang.reflect.Method;
 
public class ReflectionHelloWorld {
	public static void main(String[] args){
		Foo f = new Foo();
		System.out.println(f.getClass().getName());			
	}
}
 
class Foo {
	public void print() {
		System.out.println("abc");
	}
}
</pre>

对不知道的对象执行方法
<pre>
public class ReflectionHelloWorld {
	public static void main(String[] args){
		Foo f = new Foo();
 
		Method method;
		try {
			method = f.getClass().getMethod("print", new Class<?>[0]);
			method.invoke(f);
		} catch (Exception e) {
			e.printStackTrace();
		}			
	}
}
 
class Foo {
	public void print() {
		System.out.println("abc");
	}
}
</pre>

从类实例创建对象
<pre>
public class ReflectionHelloWorld {
	public static void main(String[] args){
		//create instance of "Class"
		Class<?> c = null;
		try{
			c=Class.forName("myreflection.Foo");
		}catch(Exception e){
			e.printStackTrace();
		}
 
		//create instance of "Foo"
		Foo f = null;
 
		try {
			f = (Foo) c.newInstance();
		} catch (Exception e) {
			e.printStackTrace();
		}	
 
		f.print();
	}
}
 
class Foo {
	public void print() {
		System.out.println("abc");
	}
}
</pre>
获取构造器和创建实例
<pre>
public class ReflectionHelloWorld {
	public static void main(String[] args){
		//create instance of "Class"
		Class<?> c = null;
		try{
			c=Class.forName("myreflection.Foo");
		}catch(Exception e){
			e.printStackTrace();
		}
 
		//create instance of "Foo"
		Foo f1 = null;
		Foo f2 = null;
 
		//get all constructors
		Constructor<?> cons[] = c.getConstructors();
 
		try {
			f1 = (Foo) cons[0].newInstance();
			f2 = (Foo) cons[1].newInstance("abc");
		} catch (Exception e) {
			e.printStackTrace();
		}	
 
		f1.print();
		f2.print();
	}
}
 
class Foo {
	String s; 
 
	public Foo(){}
 
	public Foo(String s){
		this.s=s;
	}
 
	public void print() {
		System.out.println(s);
	}
}
</per>
还可以通过实例获得接口、超类等。

改变数组长度
<pre>
public class ReflectionHelloWorld {
	public static void main(String[] args) {
		int[] intArray = { 1, 2, 3, 4, 5 };
		int[] newIntArray = (int[]) changeArraySize(intArray, 10);
		print(newIntArray);
 
		String[] atr = { "a", "b", "c", "d", "e" };
		String[] str1 = (String[]) changeArraySize(atr, 10);
		print(str1);
	}
 
	// change array size
	public static Object changeArraySize(Object obj, int len) {
		Class<?> arr = obj.getClass().getComponentType();
		Object newArray = Array.newInstance(arr, len);
 
		//do array copy
		int co = Array.getLength(obj);
		System.arraycopy(obj, 0, newArray, 0, co);
		return newArray;
	}
 
	// print
	public static void print(Object obj) {
		Class<?> c = obj.getClass();
		if (!c.isArray()) {
			return;
		}
 
		System.out.println("\nArray length: " + Array.getLength(obj));
 
		for (int i = 0; i < Array.getLength(obj); i++) {
			System.out.print(Array.get(obj, i) + " ");
		}
	}
}
</pre>


