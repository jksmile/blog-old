
#web.xml 简介【4】

## distributable 配置介绍


	<?xml version="1.0" encoding="UTF-8"?>
		<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         	xmlns="http://java.sun.com/xml/ns/javaee"
         	xsi:schemaLocation="http://java.sun.com/xml/ns/javaee
         	http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd"
         	id="web" version="2.5”>

		<!-- 站点ICON图标 -->
		<icon>

            <smalle-icon> /static/img/smalle.jpg </smalle-icon>

            <large-icon> /static/img/large.jpg <//large-icon>

		</icon>


		<!-- 应用名称 -->
		<display-name> Web </display-name>


		<!-- 描述 -->
		<descriptioin> </description>


		<!-- 分布处处理 -->
		<distributable />



	</web-app>



**[web.xml文件范例](./webxml)中有如下一段描述：**


    <!--
    The distributable element, by its presence in a web application
    deployment descriptor, indicates that this web application is
    programmed appropriately to be deployed into a distributed servlet
    container

    Used in: web-app
    -->
    <!ELEMENT distributable EMPTY>


\<distributable>元素为空标签,它的存在与否可以指定站台是否可分布式处理.

如果web.xml中出现这个元素,则代表站台在开发时已经被设计为能在多个JSP Container 之间分散执行.

***

本篇所属：[java web篇](./Java/web/Index)

上一篇：[web.xml简介【3】之description介绍](./webxml-description)

下一篇：[web.xml简介【5】之context-param介绍](./webxml-context-param)