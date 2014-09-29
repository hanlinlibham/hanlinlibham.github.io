---
layout: post
category: "algorithm"
title:  "快速排序"
tags: [algorithm|sort]
---
####1.基本步骤
-  分解：数组A[p..r]被划分为2个子数组[p..q-1]，[q+1..r]，使得左边都小于q，右边大于q；
-  解决：递归调用快速排序，对2个子数组排序；
-  合并：子数组是原址的，不需要合并；
####2.算法

{% highlight java %}
QUICKSORT(A,p,r) //初始调用A,1,A.length
if p < r
  q = PARTITION(A,p,r)
  QUICKSORT(A,p,q-1)
  QUICKSORT(A,q+1,r)

//对子数组的原址重排
//N.Lomuto的算法
PARTITION(A,p,r)
x = A[r]
i = p-1
for j = p to r-1
  if A[j]<=x
  i = i + 1
  exchange A[i] with A[j]
exchange A[i+1] with A[r]
return i+1
{% endhighlight %}

{% highlight java %}
//最早Hoare的算法
PARTITION(A,p,r)
x = A[p]
i = p-1
j = r+1
while TRUE
  repeat
    j--
  until A[j]>x
  repeat
    i++
  until A[i]<x
  if i<j
    exchange A[i] with A[j]
  else
    return j
{% endhighlight %}
####3.实现
{% highlight java %}
public static void quickSort(int[] a, int start, int end) {
    if(start<end){
        int mid = partition(a,start,end);
        quickSort(a,start,mid-1);
        quickSort(a,mid+1,end);
    }
}
private static int partition(int[] a, int start, int end) {
    int x = a[end];
    int i = start-1;
    for (int j = start; j < end; j++) {
        if(a[j]<=x){
            i++;
            exchange(a,i,j);
        }
    }
    exchange(a,i+1,end);
    return i+1;
}
//or
private static int partition(int[] a, int start, int end) {
  int x = a[start];
  int i = start - 1;
  int j = end + 1;
  while (true) {
    do {
      j--;
    } while (a[j] > x);
    do {
      i++;
    } while (a[i] < x);
    if (i < j) {
      exchange(a, i, j);
    } else {
      return j;
    }
  }
}
{% endhighlight %}
>平均O(nlgn)，最坏O(n^2)即2个子数组1个为0；