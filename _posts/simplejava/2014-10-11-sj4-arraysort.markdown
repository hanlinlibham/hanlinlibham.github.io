---
layout: post
category: "java"
title:  "[SimpleJava]-深入理解Arrays.sort"
tags: [simplejava]
---

Arrays.sort(T[], Comparator < ? super T > c) ,直接上例子：

{% highlight java %}
import java.util.Arrays;
import java.util.Comparator;
 
class Dog{
	int size;	
	public Dog(int s){
		size = s;
	}
}
 
class DogSizeComparator implements Comparator<Dog>{
 
	@Override
	public int compare(Dog o1, Dog o2) {
		return o1.size - o2.size;
	}
}
 
public class ArraySort {
 
	public static void main(String[] args) {
		Dog d1 = new Dog(2);
		Dog d2 = new Dog(1);
		Dog d3 = new Dog(3);
 
		Dog[] dogArray = {d1, d2, d3};
		printDogs(dogArray);
 
		Arrays.sort(dogArray, new DogSizeComparator());	
		printDogs(dogArray);
	}
 
	public static void printDogs(Dog[] dogs){
		for(Dog d: dogs)
			System.out.print(d.size + " " );
 
		System.out.println();
	}
}
{% endhighlight %}

Arrays.sort()使用的是装饰模式。装饰模式是在运行时动态选择不同的算法。sort方法同样可以选择不同的排序方式。看例子：

{% highlight java %}
class Dog{
	int size;
	int weight;
 
	public Dog(int s, int w){
		size = s;
		weight = w; 
	}
}
 
class DogSizeComparator implements Comparator<Dog>{
 
	@Override
	public int compare(Dog o1, Dog o2) {
		return o1.size - o2.size;
	}
}
 
class DogWeightComparator implements Comparator<Dog>{
 
	@Override
	public int compare(Dog o1, Dog o2) {
		return o1.weight - o2.weight;
	}
}
 
public class ArraySort {
 
	public static void main(String[] args) {
		Dog d1 = new Dog(2, 50);
		Dog d2 = new Dog(1, 30);
		Dog d3 = new Dog(3, 40);
 
		Dog[] dogArray = {d1, d2, d3};
		printDogs(dogArray);
 
		Arrays.sort(dogArray, new DogSizeComparator());	
		printDogs(dogArray);
 
		Arrays.sort(dogArray, new DogWeightComparator());	
		printDogs(dogArray);
	}
 
	public static void printDogs(Dog[] dogs){
		for(Dog d: dogs)
			System.out.print("size="+d.size + " weight=" + d.weight + " ");
 
		System.out.println();
	}
}
{% endhighlight %}

方法中第二个参数Comparator< ? super T > c ， < ? super T >意思是可以使用T类型的超类。为什么容许超类？答案是：这样可以让所有的子类使用相同的Comparator。看例子：

{% highlight java %}
class Animal{
	int size;
}
 
class Dog extends Animal{
	public Dog(int s){
		size = s;
	}
}
 
class Cat extends Animal{
	public Cat(int s){
		size  = s;
	}
}
 
class AnimalSizeComparator implements Comparator<Animal>{
 
	@Override
	public int compare(Animal o1, Animal o2) {
		return o1.size - o2.size;
	}
	//in this way, all sub classes of Animal can use this comparator.
}
 
public class ArraySort {
 
	public static void main(String[] args) {
		Dog d1 = new Dog(2);
		Dog d2 = new Dog(1);
		Dog d3 = new Dog(3);
 
		Dog[] dogArray = {d1, d2, d3};
		printDogs(dogArray);
 
		Arrays.sort(dogArray, new AnimalSizeComparator());	
		printDogs(dogArray);
 
		System.out.println();
 
		//when you have an array of Cat, same Comparator can be used. 
		Cat c1 = new Cat(2);
		Cat c2 = new Cat(1);
		Cat c3 = new Cat(3);
 
		Cat[] catArray = {c1, c2, c3};
		printDogs(catArray);
 
		Arrays.sort(catArray, new AnimalSizeComparator());	
		printDogs(catArray);
	}
 
	public static void printDogs(Animal[] animals){
		for(Animal a: animals)
			System.out.print("size="+a.size + " ");
		System.out.println();
	}
}
{% endhighlight %}

总结一下：

* 一般的，super的

* 装饰模式

* mergesort nlogn时间复杂度

* Java.util.Collections#sort方法和它类似。