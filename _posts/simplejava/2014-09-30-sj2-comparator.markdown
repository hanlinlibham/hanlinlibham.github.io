---
layout: post
category: "java"
title:  "[SimpleJava]-Comparable vs Comparator "
tags: [simplejava]
---
####1.Comparable
在要排序的类内部实现
{% highlight java %}
class HDTV implements Comparable<HDTV> {
	private int size;
	private String brand;
	public int getSize() {
		return size;
	}
	public void setSize(int size) {
		this.size = size;
	}
	@Override
	public int compareTo(HDTV tv) {
		if (this.getSize() > tv.getSize())
			return 1;
		else if (this.getSize() < tv.getSize())
			return -1;
		else
			return 0;
	}
}
{% endhighlight %}
####2.Comparator
外部实现，定义一个单独的comparator
{% highlight java %}
//TV...
class SizeComparator implements Comparator<HDTV> {
	@Override
	public int compare(HDTV tv1, HDTV tv2) {
		int tv1Size = tv1.getSize();
		int tv2Size = tv2.getSize();
 
		if (tv1Size > tv2Size) {
			return 1;
		} else if (tv1Size < tv2Size) {
			return -1;
		} else {
			return 0;
		}
	}
}
//
Collections.sort(al, new SizeComparator());
{% endhighlight %}
####3.使用哪个
>Comparable 是在集合内部定义的方法实现的排序，Comparator 是在集合外部实现的排序，所以，如想实现排序，要么要排序类实现Comparable，要么定义一个外部的Comparator。String、Integer等已经实现了Comparable接口。
