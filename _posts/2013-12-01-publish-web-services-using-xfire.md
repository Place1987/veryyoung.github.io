---
layout: post
title: XFire发布Web Services
date: 2013-12-01 17:07
author: VERYYOUNG
comments: true
categories: [Web Service]
---
最近在学习web services，网上先关的资料不多，讲的都是很基础，例子也很简单，自己动手敲了敲在这里和大家分享一下，希望能对初学者有所帮助。


Web Services服务器端开发

服务器端开发用的是XFire，版本是1.2.6,XFire现在已经成apache下面的一个项目CXF的一部分了，老早就不更新版本了，XFire过不过时我是不知道，不过还有一些人在用。

开发环境是：IDEA,Tomcat 8.0

新建一个项目，可以是web project也可以是web service project，区别不大。项目建好之后：（项目名假设为：webservice）

1、下载XFire1.2.6.jar

加压下载好的文件，将lib文件夹下所有jar包添加到项目中，并且将xfire-all-1.2.6.jar加入到项目中。
下载地址 http://xfire.codehaus.org/

2、编写服务接口

	public interface CalculatorService {
	    public int add(int a,int b);
	    public int sub(int a,int b);
	    public int mul(int a,int b);
	    public int div(int a,int b);
	}


3、编写服务接口实现类

	public class CalculatorServiceImpl implements CalculatorService{
	
	    @Override
	    public int add(int a, int b) {
	        return  a+b;  //To change body of implemented methods use File | Settings | File Templates.
	    }
	
	    @Override
	    public int sub(int a, int b) {
	        return a-b;  //To change body of implemented methods use File | Settings | File Templates.
	    }
	
	    @Override
	    public int mul(int a, int b) {
	        return a*b;  //To change body of implemented methods use File | Settings | File Templates.
	    }
	
	    @Override
	    public int div(int a, int b) {
	        return a/b;  //To change body of implemented methods use File | Settings | File Templates.
	    }
	}


4、编写web.xml

	
	<?xml version="1.0" encoding="UTF-8"?>
	<web-app xmlns="http://java.sun.com/xml/ns/javaee"
	         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	         xsi:schemaLocation="http://java.sun.com/xml/ns/javaee
			  http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd"
	         version="3.0">
	    <servlet>
	        <servlet-name>XFireServlet</servlet-name>
	        <servlet-class>org.codehaus.xfire.transport.http.XFireConfigurableServlet</servlet-class>
	        <load-on-startup>0</load-on-startup>
	    </servlet>
	
	    <servlet-mapping>
	        <servlet-name>XFireServlet</servlet-name>
	        <url-pattern>/services/*</url-pattern>
	    </servlet-mapping>
	
	    <servlet-mapping>
	        <servlet-name>XFireServlet</servlet-name>
	        <url-pattern>/services/XFireServlet/*</url-pattern>
	    </servlet-mapping>
	
	    <welcome-file-list>
	        <welcome-file>index.jsp</welcome-file>
	    </welcome-file-list>
	
	</web-app>



5、配置服务

在src目录下新建WEB-INF文件夹，在WEB-INF文件夹下新建xfire文件夹，在xfire下新建services.xml文件。

name表示服务的名字可以自己随便定义，serviceClass指明服务接口类，implementationClass指明服务实现类


	<?xml version="1.0" encoding="UTF-8"?>
	<beans xmlns="http://xfire.codehaus.org/config/1.0">
	    <service>
	        <name>CalculatorService</name>
	        <serviceClass>com.young.service.CalculatorService</serviceClass>
	        <implementationClass>
	            com.young.service.CalculatorServiceImpl
	        </implementationClass>
	
	    </service>
	</beans>


6、启动服务

将该项目添加到tomcat中，启动tomcat，在浏览器中输入http://localhost:8080/webservice/services就能看到该项目下所有服务，点击服务后面的[wsdl]，就会看到服务的wsdl文件内容。
<img src="http://veryyoung.u.qiniudn.com/7niu_wsdl.png" alt="" />

6、编写客户端
通过WSDL地址来创建动态客户端,代码如下

	public class ClientTest {
	    public static void main(String[] args) throws Exception {
	        Client client = new Client(new URL("http://localhost:8080/webservice/services/CalculatorService?wsdl"));
	        Object[] results = client.invoke("add", new Object[]{1, 2});
	        System.out.println(results[0]);
	    }
	}



项目文件目录结构如下：
<img src="http://veryyoung.u.qiniudn.com/7niu_forder.png" alt="" />

7.跨语言编写客户端

前面编写的客户端采用的是java语言，与Service采用的是同一个JVM，无法直观的体会出webservice跨平台跨语言的特性
下面采用c#编写客户端
打开Visual Studio，新建一个c# console project，命名为wsclient，添加引用，选择添加web引用，输入http://localhost:8080/webservice/services/CalculatorService?wsdl
给该引用命名为CalculatorService
编写测试代码，代码如下


	using System;
	using System.Collections.Generic;
	using System.Linq;
	using System.Text;
	using wsclient.CalculatorService;
	
	namespace wsclient
	{
	    class Program
	    {
	        static void Main(string[] args)
	        {
	            CalculatorService.CalculatorService cal = new CalculatorService.CalculatorService();
	            int result = cal.add(1, 2);
	            Console.WriteLine(result);
	            Console.ReadKey();
	        }
	    }
	}

点击运行，效果如下
<img src="http://veryyoung.u.qiniudn.com/7niu_csharpconsole.png" alt="" />

