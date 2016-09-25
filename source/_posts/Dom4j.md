---
title: Dom4j
date: 2016-05-06 19:31:58
tags:
	Dom4j
---
Dom for Java
整合了Dom和sax两种思想。读取采用了sax思想，又参照Dom思想在内存中创建了一颗对象关系树。

```
SAXReader reader = new SAXReader();
Document document = reader.read(url);
```

# 读取XML
在`src`下创建`students.xml`文件：

<!--more-->

```
<?xml version="1.0" encoding="UTF-8"?>
<students> 
	<student number="0001"> 
    	<name>tom</name>  
    	<age>17</age>  
    	<sex>male</sex> 
  	</student>  
  	<student number="0002"> 
    	<name>rose</name>  
   		<age>16</age>  
    	<sex>female</sex> 
  	</student>  
  	<student name="0003"> 
    	<name>join</name>  
    	<age>age</age>  
    	<sex>sex</sex> 
  	</student> 
</students>
```

java文件：
```
package cn.arthas.dom4j;

import java.io.File;

import org.dom4j.Document;
import org.dom4j.DocumentException;
import org.dom4j.io.SAXReader;

//读取XML
public class Demo1 {
	public static void main(String[] args) {
		SAXReader reader = new SAXReader();
        try {
			Document document = reader.read(new File("src/students.xml"));
			System.out.println(document.asXML());
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}
```

# 查询所有学生信息
```
package cn.arthas.dom4j;

import java.io.File;
import java.util.Iterator;

import org.dom4j.Document;
import org.dom4j.DocumentException;
import org.dom4j.Element;
import org.dom4j.io.SAXReader;

//查询出所有学生的所有信息 
public class Demo2 {
	public static void main(String[] args) {
		SAXReader reader = new SAXReader();
        try {
			Document document = reader.read(new File("src/students.xml"));
			
		//1 获得根元素
			Element root = document.getRootElement();
		//2迭代根元素下的所有名叫student的子元素
			for(Iterator<Element> it = root.elementIterator("student");it.hasNext();){
				Element student = it.next();
		//3获得student元素的number属性
				String number = student.attributeValue("number");
		//4student子元素的内容（name age sex）
				String name = student.elementText("name");
				String age = student.elementText("age");
				String sex = student.elementText("sex");
				
				System.out.println("当前学生的学号是"+number+",姓名是："+name+",年龄是："+age+",性别是："+sex);
			}
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}

```
# 增加一个学生元素，`join 0003 16 male`
```
package cn.arthas.dom4j;

import java.io.File;
import java.io.FileWriter;
import java.io.PrintWriter;
import java.util.Iterator;

import org.dom4j.Document;
import org.dom4j.DocumentException;
import org.dom4j.Element;
import org.dom4j.io.OutputFormat;
import org.dom4j.io.SAXReader;
import org.dom4j.io.XMLWriter;

//增加一个学生元素，join 0003 16 male
public class Demo3 {
	public static void main(String[] args) {
		SAXReader reader = new SAXReader();
        try {
			Document document = reader.read(new File("src/students.xml"));
		//1 获得根元素
			Element root = document.getRootElement();
		//2添加Element  添加number属性
			Element studentEle = root.addElement("student").addAttribute("name", "0003");
		//3添加name age sex子元素，并添加子元素中的文本
			studentEle.addElement("name").addText("join");
			studentEle.addElement("age").addText("age");
			studentEle.addElement("sex").addText("sex");
		//4将document对象写到文件中
			OutputFormat format = OutputFormat.createPrettyPrint();  //创建格式化器
			format.setEncoding("utf-8");  //指定XML文件读取的编码
//			XMLWriter writer = new XMLWriter(new FileWriter("src/students.xml"),format);//创建写入器
			XMLWriter writer = new XMLWriter(new PrintWriter("src/students.xml","utf-8"),format); //指定写入的编码
			writer.write(document);  //写入
			writer.close();			//关闭资源
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}

```

# 删除一个学生  编号为0001
```
package cn.arthas.dom4j;

import java.io.File;
import java.io.FileOutputStream;
import java.io.FileWriter;
import java.io.PrintWriter;
import java.util.Iterator;

import org.dom4j.Document;
import org.dom4j.DocumentException;
import org.dom4j.Element;
import org.dom4j.io.OutputFormat;
import org.dom4j.io.SAXReader;
import org.dom4j.io.XMLWriter;

//删除一个学生 0001
public class Demo4 {
	public static void main(String[] args) {
		SAXReader reader = new SAXReader();
        try {
			Document document = reader.read(new File("src/students.xml"));
		//1 获得根元素
			Element root = document.getRootElement();
		//使用Xpath找到我们需要的元素
			//定义Xpath
			String xpath = "//student[@number='0001']";
			Element student = (Element) document.selectSingleNode(xpath);
		//删除
			System.out.println(student.getParent().remove(student));
		//回写
			XMLWriter writer = new XMLWriter(new FileOutputStream("src/students.xml"),OutputFormat.createPrettyPrint());
			writer.write(document);
			writer.close();
			
			
		//可以用，但是效率不高
			//2获得所有学生元素
			//3判断number属性是否为要删除的
			//4回写
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}

```
# 修改一个学生  `0002 ==> rose 16 female`
```
package cn.arthas.dom4j;

import java.io.File;
import java.io.FileOutputStream;
import java.io.FileWriter;
import java.io.PrintWriter;
import java.util.Iterator;

import org.dom4j.Document;
import org.dom4j.DocumentException;
import org.dom4j.Element;
import org.dom4j.io.OutputFormat;
import org.dom4j.io.SAXReader;
import org.dom4j.io.XMLWriter;

//修改一个学生 0002 ==> rose 16 female
public class Demo5 {
	public static void main(String[] args) {
		SAXReader reader = new SAXReader();
        try {
			Document document = reader.read(new File("src/students.xml"));
		//1定义xpath表达式
			String xpath = "//student[@number='0002']";
		//2使用xpath查找
			Element studentEle = (Element) document.selectSingleNode(xpath);
		//3修改student元素的name age sex
			studentEle.element("name").setText("rose");
			studentEle.element("age").setText("16");
			studentEle.element("sex").setText("female");
		//回写
			XMLWriter writer = new XMLWriter(new FileOutputStream("src/students.xml"),OutputFormat.createPrettyPrint());
			writer.write(document);
			writer.close();
			
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}

```
