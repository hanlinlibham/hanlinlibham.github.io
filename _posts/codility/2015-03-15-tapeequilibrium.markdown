---
layout: post
category: "codility"
title:  "[codility]TapeEquilibrium"
tags: [codility]
---
#### TapeEquilibrium

一个数组，找到其中一点p，使得被p划分的左右2个子数组的和，他们的差值绝对值最小。
比如数组{3,1，2,43}，p=3时，|6-7|=1最小。

#### 分析

先设定p=1，把数组分为a[0]和后面的之和，然后依次把后面的一个元素移动到前子数组，比较差值的绝对值。

<pre>
public int solution(int[] A) {
	int N = A.length;
	int sum1 = A[0];
	int sum2 = 0;
	int P = 1;
	for (int i = P; i < N; i++) {
		sum2 += A[i];
	}
	int diff = Math.abs(sum1 - sum2);
	for (; P < N - 1; P++) {
		sum1 += A[P];
		sum2 -= A[P];
		int newDiff = Math.abs(sum1 - sum2);
		if (newDiff < diff) {
			diff = newDiff;
		}
	}
	return diff;
}
</pre>
<p>{{ page.date | date_to_string }}</p>
