---
layout: post
category: "java"
title:  "[SimpleJava]-逐行写文件"
tags: [simplejava]
---
方法1 FileOutputStream

<pre>
public static void writeFile1() throws IOException {
    File fout = new File("out.txt");
    FileOutputStream fos = new FileOutputStream(fout);
 
    BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(fos));
 
    for (int i = 0; i < 10; i++) {
        bw.write("something");
        bw.newLine();
    }
 
    bw.close();
}
</pre>

方法2 FileWriter

<pre>
public static void writeFile2() throws IOException {
    FileWriter fw = new FileWriter("out.txt");
 
    for (int i = 0; i < 10; i++) {
        fw.write("something");
    }
 
    fw.close();
}
</pre>

方法3 PrintWriter
<pre>
public static void writeFile3() throws IOException {
    PrintWriter pw = new PrintWriter(new FileWriter("out.txt"));
 
    for (int i = 0; i < 10; i++) {
        pw.write("something");
    }
 
    pw.close();
}
</pre>

方法4 OutputStreamWriter
<pre>
public static void writeFile4() throws IOException {
    File fout = new File("out.txt");
    FileOutputStream fos = new FileOutputStream(fout);
 
    OutputStreamWriter osw = new OutputStreamWriter(fos);
 
    for (int i = 0; i < 10; i++) {
        osw.write("something");
    }
 
    osw.close();
}
</pre>

FileWriter/PrintWriter的区别：前者抛IO异常。后者提供了一些额外的格式化方法如println方便在不同平台换行。PrintWriter自动执行flush。


