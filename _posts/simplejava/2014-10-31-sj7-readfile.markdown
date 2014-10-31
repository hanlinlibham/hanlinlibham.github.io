---
layout: post
category: "java"
title:  "[SimpleJava]-逐行读取文件"
tags: [simplejava]
---
方法1

<pre>
private static void readFile1(File fin) throws IOException {
    FileInputStream fis = new FileInputStream(fin);
 
    //Construct BufferedReader from InputStreamReader
    BufferedReader br = new BufferedReader(new InputStreamReader(fis));
 
    String line = null;
    while ((line = br.readLine()) != null) {
        System.out.println(line);
    }
 
    br.close();
}
</pre>

方法2

<pre>
private static void readFile2(File fin) throws IOException {
    // Construct BufferedReader from FileReader
    BufferedReader br = new BufferedReader(new FileReader(fin));
 
    String line = null;
    while ((line = br.readLine()) != null) {
        System.out.println(line);
    }
 
    br.close();
}
</pre>

文件获取代码：
<pre>
//use . to get current directory
File dir = new File(".");
File fin = new File(dir.getCanonicalPath() + File.separator + "in.txt");
 
readFile1(fin);
readFile2(fin);
</pre>

两者的不同是神马？官方文档中的描述大概翻译下：

InputStreamReader是字节流到字符流的桥梁，按定义的编码读取字节并变成字符。它可以处理文件、网络等流。

FileReader是一个按字符读取文件的类。它不容许你定义平台默认编码之外的编码。所以如果代码要运行在不同的系统编码环境下使用reader不是个好主意。

总之InputStream要比Reader安全。

注意一下File.separator，不同的操作系统文件分隔符会不同，使用这个很安全。

在java1.7之后，可以使用下面的代码，本质是一样的：

<pre>
Charset charset = Charset.forName("US-ASCII");
try (BufferedReader reader = Files.newBufferedReader(file, charset)) {
    String line = null;
    while ((line = reader.readLine()) != null) {
        System.out.println(line);
    }
} catch (IOException x) {
    System.err.format("IOException: %s%n", x);
}
</pre>

Files.newBufferedReader源码：
<pre>
public static BufferedReader newBufferedReader(Path path, Charset cs){
 CharsetDecoder decoder = cs.newDecoder();
 Reader reader = new InputStreamReader(newInputStream(path), decoder);
 return new BufferedReader(reader);
}
</pre>

