---
layout: post
category: "java"
title:  "java数组10大常用功能"
tags: [java]
---
#### 1. 数组声明

<pre>
String[] aArray = new String[5];
String[] bArray = {"a","b","c", "d", "e"};
String[] cArray = new String[]{"a","b","c","d","e"};
</pre>

#### 2. 打印

<pre>
int[] intArray = { 1, 2, 3, 4, 5 };
String intArrayString = Arrays.toString(intArray);
// print directly will print reference value
System.out.println(intArray);
// [I@7150bd4d
System.out.println(intArrayString);
// [1, 2, 3, 4, 5]
</pre>

#### 3. 数组转list

<pre>
String[] stringArray = { "a", "b", "c", "d", "e" };
ArrayList<String> arrayList = new ArrayList<String>(Arrays.asList(stringArray));
System.out.println(arrayList);
// [a, b, c, d, e]
</pre>

#### 4. 检测是否有某值

<pre>
String[] stringArray = { "a", "b", "c", "d", "e" };
boolean b = Arrays.asList(stringArray).contains("a");
System.out.println(b);
// true
</pre>

#### 5. 连接2个数组

<pre>
int[] intArray = { 1, 2, 3, 4, 5 };
int[] intArray2 = { 6, 7, 8, 9, 10 };
// Apache Commons Lang library
int[] combinedIntArray = ArrayUtils.addAll(intArray, intArray2);
</pre>


#### 6. 内部声明数组

<pre>method(new String[]{"a", "b", "c", "d", "e"});</pre>

#### 7. 数组连接成一个字符串

<pre>
// containing the provided list of elements
// Apache common lang
String j = StringUtils.join(new String[] { "a", "b", "c" }, ", ");
System.out.println(j);
// a, b, c
</pre>

#### 8. list转数组

<pre>
String[] stringArray = { "a", "b", "c", "d", "e" };
ArrayList<String> arrayList = new ArrayList<String>(Arrays.asList(stringArray));
String[] stringArr = new String[arrayList.size()];
arrayList.toArray(stringArr);
</pre>

#### 9. 数组转Set

<pre>
Set<String> set = new HashSet<String>(Arrays.asList(stringArray));
</pre>

#### 10. 数组倒置

<pre>
ArrayUtils.reverse(intArray);
</pre>

#### 11. 删除元素

<pre>
int[] intArray = { 1, 2, 3, 4, 5 };
int[] removed = ArrayUtils.removeElement(intArray, 3);//create a new array
</pre>

#### int转byte数组

<pre>
byte[] bytes = ByteBuffer.allocate(4).putInt(8).array(); //8 is number
 
for (byte t : bytes) {
   System.out.format("0x%x ", t);
}
</pre>







