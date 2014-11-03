---
layout: post
category: "java"
title:  "[SimpleJava]-properties文件的使用"
tags: [simplejava]
---

<pre>
import java.io.IOException;
import java.util.Properties;
 
public class Test {
 
	public static void main(String[] args) {
		Properties configFile = new Properties();
		try {
			configFile.load(Test.class.getClassLoader().getResourceAsStream("config.properties"));
			String name = configFile.getProperty("name");
			System.out.println(name);
		} catch (IOException e) {
 
			e.printStackTrace();
		}
	}
 
}
</pre>