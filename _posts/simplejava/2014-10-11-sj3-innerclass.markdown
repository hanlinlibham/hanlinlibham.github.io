---
layout: post
category: "java"
title:  "[SimpleJava]-内部类"
tags: [simplejava]
---
>java 有4种内部类。

####1.静态内部类

{% highlight java %}
class Outer {
	static class Inner {
		void go() {
			System.out.println("Inner class reference is: " + this);
		}
	}
}
 
public class Test {
	public static void main(String[] args) {
		Outer.Inner n = new Outer.Inner();
		n.go();
	}
}
{% endhighlight %}

####2.成员内部类

可以访问外部类所有的方法和字段。

{% highlight java %}
public class Outer {
    private int x = 100;
 
    public void makeInner(){
        Inner in = new Inner();
        in.seeOuter();
    }
 
    class Inner{
        public void seeOuter(){
            System.out.println("Outer x is " + x);
            System.out.println("Inner class reference is " + this);
            System.out.println("Outer class reference is " + Outer.this);
        }
    }
 
    public static void main(String [] args){
    	Outer o = new Outer();
        Inner i = o.new Inner();
        i.seeOuter();
    }
}
{% endhighlight %}

####3.方法内部类

{% highlight java %}
public class Outer {
	private String x = "outer";
 
	public void doStuff() {
		class MyInner {
			public void seeOuter() {
				System.out.println("x is " + x);
			}
		}
 
		MyInner i = new MyInner();
		i.seeOuter();
	}
 
	public static void main(String[] args) {
		Outer o = new Outer();
		o.doStuff();
	}
}
{% endhighlight %}

{% highlight java %}
public class Outer {
	private static String x = "static outer";
 
	public static void doStuff() {
		class MyInner {
			public void seeOuter() {
				System.out.println("x is " + x);
			}
		}
 
		MyInner i = new MyInner();
		i.seeOuter();
	}
 
	public static void main(String[] args) {
		Outer.doStuff();
	}
}
{% endhighlight %}

####4.匿名类

一般使用在GUI Listener 。 

{% highlight java %}
button.addActionListener(new ActionListener(){
     public void actionPerformed(ActionEvent e){
         comp.setText("Button has been clicked");
     }
});
{% endhighlight %}
