---
layout: post
category: "java"
title:  "[SimpleJava]-wait() && notify()"
tags: [simplejava]
---
#### 1. 背景知识

* synchronized用来保证独占访问。
* 同一个对象的同步方法不能交叉。
* 同步块声明的对象必须是本身的锁，当同步this时，必须避免同步其他对象的方法。
* wait告诉线程放弃监听去等待，直到进入同一对象的其他线程调用notify。
* notify唤醒调用wait的第一个线程。

#### 2. code1
<pre>
public class ThreadA {
    public static void main(String[] args){
        ThreadB b = new ThreadB();
        b.start();
 
        synchronized(b){
            try{
                System.out.println("Waiting for b to complete...");
                b.wait();
            }catch(InterruptedException e){
                e.printStackTrace();
            }
 
            System.out.println("Total is: " + b.total);
        }
    }
}
 
class ThreadB extends Thread{
    int total;
    @Override
    public void run(){
        synchronized(this){
            for(int i=0; i<100 ; i++){
                total += i;
            }
            notify();
        }
    }
}
</pre>
这个例子中线程b在完成计算后主线程才输出。如果b没有同步，那么输出计算不正确。
<pre>
public class ThreadA {
	public static void main(String[] args) {
		ThreadB b = new ThreadB();
		b.start();
 
		System.out.println("Total is: " + b.total);
 
	}
}
 
class ThreadB extends Thread {
	int total;
 
	@Override
	public void run() {
		for (int i = 0; i < 100; i++) {
			total += i;
		}
	}
}
</pre>

#### 3. code2

<pre>
import java.util.Vector;
 
class Producer extends Thread {
 
    static final int MAXQUEUE = 5;
    private Vector messages = new Vector();
 
    @Override
    public void run() {
        try {
            while (true) {
                putMessage();
                //sleep(5000);
            }
        } catch (InterruptedException e) {
        }
    }
 
    private synchronized void putMessage() throws InterruptedException {
        while (messages.size() == MAXQUEUE) {
            wait();
        }
        messages.addElement(new java.util.Date().toString());
        System.out.println("put message");
        notify();
        //Later, when the necessary event happens, the thread that is running it calls notify() from a block synchronized on the same object.
    }
 
    // Called by Consumer
    public synchronized String getMessage() throws InterruptedException {
        notify();
        while (messages.size() == 0) {
            wait();//By executing wait() from a synchronized block, a thread gives up its hold on the lock and goes to sleep.
        }
        String message = (String) messages.firstElement();
        messages.removeElement(message);
        return message;
    }
}
 
class Consumer extends Thread {
 
    Producer producer;
 
    Consumer(Producer p) {
        producer = p;
    }
 
    @Override
    public void run() {
        try {
            while (true) {
                String message = producer.getMessage();
                System.out.println("Got message: " + message);
                //sleep(200);
            }
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
 
    public static void main(String args[]) {
        Producer producer = new Producer();
        producer.start();
        new Consumer(producer).start();
    }
}
</pre>

这个例子模拟一个定长的阻塞队列，可能的输出：
<pre>
put message
put message
put message
Got message: Wed Oct 29 11:45:37 CST 2014
put message
Got message: Wed Oct 29 11:45:37 CST 2014
put message
Got message: Wed Oct 29 11:45:37 CST 2014
</pre>

