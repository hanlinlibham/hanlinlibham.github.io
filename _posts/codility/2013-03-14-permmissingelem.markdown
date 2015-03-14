---
layout: post
category: "codility"
title:  "[codility]PermMissingElem"
tags: [codility]
---
#### 题目 PermMissingElem

有一个包含N个元素的数组，元素是[1..N+1]，找出缺失的那个。

#### 分析

之前遇到这个题直接就想到了高斯算1到100相加的故事。解法1，遍历以便，分别对当前数组元素值求和，然后再对正常值求和，相减得结果。解法2，使用一个桶排序，没填充的那个index就是缺失的元素。但这方法需要额外的空间，同时还要再遍历桶一遍，效率稍差。

<pre>
public static int solution(int[] A) {
		int sum = 0;
		int total = 0;
		for (int i = 0; i < A.length; i++) {
			sum += A[i];
			total += i+1;
		}
		int result = total + A.length + 1 - sum;
		return result;
	}
</pre>
<p>{{ page.date | date_to_string }}</p>
