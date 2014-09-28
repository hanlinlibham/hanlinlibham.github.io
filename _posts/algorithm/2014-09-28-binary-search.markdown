---
layout: post
category: "algorithm"
title:  "二分查找算法"
tags: [algorithm|search]
---
>很久以前去某公司面试考到二分查找算法，一时半会悲剧了，平时就只知道Arrays.binarySearch直接用，不求甚解啊。

#### 非递归算法
{% highlight java %}
public static int binarySearch(int arr[], int key) {
	int low = 0, high = arr.length - 1;
	int mid;
	while (low <= high) {
		mid = (low + high) / 2;
		if (key == arr[mid])
			return mid;
		if (key < arr[mid])
			high = mid - 1;
		if (key > arr[mid])
			low = mid + 1;
	}
	return -1;
}
{% endhighlight %}

#### 递归算法
{% highlight java %}
public static int binarySearchByRecurison(int arr[], int low, int high, int key) {
	if (low <= high) {
		int mid = (low + high) / 2;
		if (key == arr[mid])
			return mid;
		if (key < arr[mid]) {
			high = mid - 1;
		} else {
			low = mid + 1;
		}
		return binarySearchByRecurison(arr, low, high, key);
	}
	return -1;
}
{% endhighlight %}
>做了下测试，2种方法的效率差不多，在不同数量级下都几乎一致。