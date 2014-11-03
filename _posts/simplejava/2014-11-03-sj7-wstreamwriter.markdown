---
layout: post
category: "java"
title:  "[SimpleJava]-FileOutputStream vs FileWriter"
tags: [simplejava]
---
写文件可以使用FileOutputStream和FileWriter

<pre>
File fout = new File(file_location_string);
FileOutputStream fos = new FileOutputStream(fout);
BufferedWriter out = new BufferedWriter(new OutputStreamWriter(fos));
out.write("something");
</pre>

<pre>
FileWriter fstream = new FileWriter(file_location_string);
BufferedWriter out = new BufferedWriter(fstream);
out.write("something");
</pre>

区别是什么？看看java规范的描述
>FileOutputStream is meant for writing streams of raw bytes such as image data. For writing streams of characters, consider using FileWriter.

主要的区别就是一个是写字节，一个写字符。FileOutputStream有个应用是把文件转换成字节数组。