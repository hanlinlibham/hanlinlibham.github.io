---
layout: post
category: "design"
title:  "简单工厂-Simple Factory"
tags: [design|factory]
---
>实际上简单工厂不是一个真正意义上的设计模式，它是一个简化版的工厂方法，但是它实在是太好用了，也非常容易理解。我自己的代码中使用最多的模式就是它。下面的类图和代码引用自[here](http://www.programcreek.com/2013/02/java-design-pattern-factory/)。

#### 1.类图
![pic1](http://www.programcreek.com/wp-content/uploads/2013/02/factory-design-pattern.png)
这是一个造人工厂，工厂有一个静态的create方法，通过不同的入参判断造男孩还是女孩。

#### 2.代码
{% highlight java %}
interface Human {
	public void Talk(); //原作者可能疏忽了，方法名给了大写。。。
	public void Walk();
}
class Boy implements Human{
	@Override
	public void Talk() {
		System.out.println("Boy is talking...");		
	}
 
	@Override
	public void Walk() {
		System.out.println("Boy is walking...");
	}
}
class Girl implements Human{
 
	@Override
	public void Talk() {
		System.out.println("Girl is talking...");	
	}
 
	@Override
	public void Walk() {
		System.out.println("Girl is walking...");
	}
}
public class HumanFactory {
	//核心代码
	public static Human createHuman(String m){
		Human p = null;
		if(m == "boy"){
			p = new Boy();
		}else if(m == "girl"){
			p = new Girl();
		}
 
		return p;
	}
}
{% endhighlight %}
>JDK里也有不少简单工厂的例子，如Calendar、NumberFormat。