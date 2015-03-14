---
layout: post
category: "java"
title:  "[SimpleJava]-线程重写"
tags: [simplejava]
---

<pre>
class A implements Runnable {
    public void run() {
        System.out.println(Thread.currentThread().getName());
    }
}
 
class B implements Runnable {
 
    public void run() {
        new A().run();
        new Thread(new A(), "name_thread2").run();
        new Thread(new A(), "name_thread3").start();
    }
}
 
public class Main {
 
    public static void main(String[] args) {
        new Thread(new B(), "name_thread1").start();
    }
}
</pre>

输出：
<pre>
name_thread1
name_thread1
name_thread3
</pre>

调用run和start的区别：start会创建新线程并执行，run在当前线程中执行。