---
layout: post
category: "design"
title:  "工厂方法"
tags: [design]
---
作者原文是抽象工厂（[l1](http://www.programcreek.com/2013/02/java-design-pattern-abstract-factory/)），实际上介绍的模式是工厂方法。

抽象工厂添加了一个抽象层，它是创建其他工厂的超类，可以称之为工厂的工厂。抽象工厂是现代框架中经常使用的。

下面的例子是一个生产cpu的工厂。

![p1](http://www.programcreek.com/wp-content/uploads/2013/02/abstract-factory-design-pattern.png)

<pre>
interface CPU {
    void process();
}
 
interface CPUFactory {
	CPU produceCPU();
	//使用方式可动态创建
	//Product createProduct(Class<? extends Product> c);
}
 
class AMDFactory implements CPUFactory {
    public CPU produceCPU() {
        return new AMDCPU();
        //product = (Product)Class.forName(c.getName()).newInstance();
    }
}
 
class IntelFactory implements CPUFactory {
    public CPU produceCPU() {
        return new IntelCPU();
    }
}
 
class AMDCPU implements CPU {
    public void process() {
        System.out.println("AMD is processing...");
    }
}
 
class IntelCPU implements CPU {
    public void process() {
        System.out.println("Intel is processing...");
    }
}
 
class Computer {
	CPU cpu;
 
    public Computer(CPUFactory factory) {
    	cpu = factory.produceCPU();
        cpu.process();
    }
}
 
public class Client {
    public static void main(String[] args) {
        new Computer(createSpecificFactory());
    }
 
    public static CPUFactory createSpecificFactory() {
        int sys = 0; // based on specific requirement
        if (sys == 0) 
        	return new AMDFactory();
        else 
        	return new IntelFactory();
    }
}
</pre>