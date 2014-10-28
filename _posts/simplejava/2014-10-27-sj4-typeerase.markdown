---
layout: post
category: "java"
title:  "[SimpleJava]-类型擦除机制"
tags: [simplejava]
---
常见错误

{% highlight java %}
public static void main(String[] args) throws IOException {
	ArrayList<String> al = new ArrayList<String>();
	al.add("a");
	al.add("b");

	accept(al);
}

public static void accept(ArrayList<Object> al){
	for(Object o: al)
		System.out.println(o);
}
{% endhighlight %}

编译不通过，返回错误信息：The method accept(ArrayList < Object > ) in the type Main is not applicable for the arguments (ArrayList < String > )

原因就是类型擦除机制。java的类型实现是在编译层面的，编译器生成的字节码不包含类型信息。上面的例子，编译后，2个list对jvm来说类型不可见，编译器发现他们不相同，所以给出了错误信息。

{% highlight java %}
public static void main(String args[]) {
    	ArrayList<Object> al = new ArrayList<Object>();
    	al.add("abc");
    	test(al);
    }
 
    public static void test(ArrayList<?> al){
    	for(Object e: al){//no matter what type, it will be Object
    		System.out.println(e);
// in this method, because we don't know what type ? is, we can not add anything to al. 
    	}
    }
{% endhighlight %}

上面的例子可以运行，使用通配符？，如果是ArrayList<?>将不能添加，因为不知道什么类型。

数组是不一样的，String[] 是Object[]的子类型，可以添加数据进去。