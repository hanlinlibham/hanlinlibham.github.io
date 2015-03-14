---
layout: post
category: "java"
title:  "top10 java集合"
tags: [java]
---
#### 1. ArrayList vs LinkedList

ArrayList实际上是个数组，元素可以用下标访问，但是满的时候需要分配一个更大的数组并移动元素，这将花费O(n)时间。添加、删除也都需要移动元素。这是它最大的弊端。

LinkedList是个双向链表。要访问一个元素需要从头开始扫描。添加删除很快。

                   | Arraylist | LinkedList
 ------------------------------------------
 get(index)        |    O(1)   |   O(n)
 add(E)            |    O(n)   |   O(1)
 add(E, index)     |    O(n)   |   O(n)
 remove(index)     |    O(n)   |   O(n)
 Iterator.remove() |    O(n)   |   O(1)
 Iterator.add(E)   |    O(n)   |   O(1)

#### 2. 迭代的删除集合元素

这是唯一正确的做法
<pre>
Iterator<Integer> itr = list.iterator();
while(itr.hasNext()) {
   // do something
   itr.remove();
}
</pre>

#### 3. 转换List到int[]

使用ArrayUtils最方便。
<pre>int[] array = ArrayUtils.toPrimitive(list.toArray(new Integer[0]));</pre>
注意不能使用List.toArray()，这将转换成Integer[]。

#### 4. 转换int[]到List

同上，
<pre>List list = Arrays.asList(ArrayUtils.toObject(array));</pre>

#### 5. 过滤集合最好的方法

可以使用三方工具类，Guava或者apache的。JDK里要困难点，不过java8已经提供了Predicate。基本方法：
<pre>
Iterator<Integer> itr = list.iterator();
while(itr.hasNext()) {
   int i = itr.next();
   if (i > 5) { // filter all ints bigger than 5
      itr.remove();
   }
}
</pre>

#### 6. 最简单的方法转换List到Set

一般的方法：
<pre>Set<Integer> set = new HashSet<Integer>(list);</pre>

如果需要特定的排序，使用下面：
<pre>
Set<Integer> set = new TreeSet<Integer>(aComparator);
set.addAll(list);
</pre>

#### 7. 从ArrayList移除重复元素

如果不关心排序，使用上面的代码放入Set即可。如果关心排序，放入LinkedHashSet。

#### 8. 排序

* Collections.sort()  排序一个list，是稳定排序，nlog(n).
* PriorityQueue  只能取得头元素，不能随机访问。
* TreeSet  基本同上，只能取头尾元素。

#### 9. Collections.emptyList() vs new instance

emptyList是不可变的（所以不能add），单例list，所有调用都重用它。

#### 10. Collections.copy

2种方法进行list的复制：
<pre>ArrayList<Integer> dstList = new ArrayList<Integer>(srcList);</pre>

另一种是Collections.copy() 
<pre>
ArrayList<Integer> dstList = new ArrayList<Integer>(srcList.size());
Collections.copy(dstList, srcList);
</pre>

2种方法都是浅复制（shallow copy）。Collections.copy方法不会给目标list重新分配内存空间，即使它不能放下所有源元素（它会抛出IndexOutOfBoundsException）。这么做的一个原因是可以保证运行在线性时间内。