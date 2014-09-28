---
layout: post
category: "java"
title:  "[SimpleJava]-检查数组中存在某个值的几种方法"
tags: [simplejava]
---
这是stackoverflow上常见的一个问题，下面看看在java中有几种方法。
1. 使用List
{% highlight java %}
Arrays.asList(arr).contains(targetValue);
{% endhighlight %}
2. 使用Set
{% highlight java %}
Set<String> set = new HashSet<String>(Arrays.asList(arr));
return set.contains(targetValue);
{% endhighlight %}
3. 循环遍历
{% highlight java %}
for(String s: arr){
	if(s.equals(targetValue))
		return true;
}
{% endhighlight %}
4. 二分查找（必须是排序过的数组）
{% highlight java %}
return Arrays.binarySearch(arr, targetValue)>=0;
{% endhighlight %}
>	这几种方法的效率如何？分别对length=5、1k、10k的数组做了测试，非有序的情况下，使用循环遍历是最快的，list和循环是一个数量级，慢了0-1倍，Set最慢，多了一个数量级。有序数组情况，二分查找最快，比循环要快了1个数量级，可见算法的威力。