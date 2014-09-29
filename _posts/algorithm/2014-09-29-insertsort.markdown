---
layout: post
category: "algorithm"
title:  "插入排序"
tags: [algorithm|sort]
---
>类似排序手中的扑克牌：从右向左与已经在手中的牌进行比较；

>适合少量数据；

>插入排序是一个不稳定的排序方法；

{% highlight java %}
//算法
for j = 2 to A.length
  key = A[j]
  //insert aj into sorted seq a(1..j-1)
  i = j - 1
  while i > 0 && A[j]>key
    A[i+1] = A[i]
    i = i - 1
  A[i+1] = key
{% endhighlight %}

{% highlight java %}
public static void insertSort(int[] value) {
    int i, j, temp;
    // 从第二个数开始，插入前面的有序序列
    for (i = 1; i < value.length; i++) {
        // 记录将要插入的记录
        temp = value[i];
        // 从该记录前面的一条记录开始比较，如果比前面的数小，那么不断后移
        for (j = i - 1; j >= 0; j--) {
            if (temp < value[j]) {
                value[j + 1] = value[j];
            } else
                break;
        }
        //放在正确的位置
        value[j + 1] = temp;
    }
}
{% endhighlight %}