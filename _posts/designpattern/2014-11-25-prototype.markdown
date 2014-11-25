---
layout: post
category: "design"
title:  "原型"
tags: [design]
---
原型就是clone一个对象然后设置改变的属性。可以节省资源。java库中的原型例子是clone；

![p1](http://www.programcreek.com/wp-content/uploads/2013/02/prototype-pattern-class-diagram.png)

<pre>
package designpatterns.prototype;
 
//prototype
interface Prototype {
    void setSize(int x);
    void printSize();
 }
 
// a concrete class
class A implements Prototype, Cloneable {
    private int size;
 
    public A(int x) {
        this.size = x;
    }
 
    @Override
    public void setSize(int x) {
        this.size = x;
    }
 
    @Override
    public void printSize() {
        System.out.println("Size: " + size);
    }
 
 
    @Override
    public A clone() throws CloneNotSupportedException {
        return (A) super.clone();
    }
}
 
//when we need a large number of similar objects
public class PrototypeTest {
    public static void main(String args[]) throws CloneNotSupportedException {
        A a = new A(1);
 
        for (int i = 2; i < 10; i++) {
            Prototype temp = a.clone();
            temp.setSize(i);
            temp.printSize();
        }
    }
}
</pre>
