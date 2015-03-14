---
layout: post
category: "java"
title:  "[SimpleJava]-序列化"
tags: [simplejava]
---
什么是序列化？就是把对象转换成字节序列，可以写入db或文件，也可以从文件读取并反序列化成对象。序列化的原因主要是要进行网络传输等，而对象包含很多内容，传输对象更方便。

<pre>
public static void main(String[] args) {
	//create an object
	Dog e = new Dog();
	e.setName("bulldog");
	e.setColor("white");
	e.setWeight(5);

	//serialize
	try {
		FileOutputStream fileOut = new FileOutputStream("./dog.ser");
		ObjectOutputStream out = new ObjectOutputStream(fileOut);
		out.writeObject(e);
		out.close();
		fileOut.close();
		System.out.printf("Serialized dog is saved in ./dog.ser");
	} catch (IOException i) {
		i.printStackTrace();
	}

	e = null;

	//Deserialize
	try {
		FileInputStream fileIn = new FileInputStream("./dog.ser");
		ObjectInputStream in = new ObjectInputStream(fileIn);
		e = (Dog) in.readObject();
		in.close();
		fileIn.close();
	} catch (IOException i) {
		i.printStackTrace();
		return;
	} catch (ClassNotFoundException c) {
		System.out.println("Dog class not found");
		c.printStackTrace();
		return;
	}

	System.out.println("\nDeserialized Dog ...");
	System.out.println("Name: " + e.getName());
	System.out.println("Color: " + e.getColor());
	System.out.println("Weight: " + e.getWeight());

	e.introduce();

}
</pre>
