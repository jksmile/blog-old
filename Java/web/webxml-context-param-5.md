
#web.xml 简介【5】

## context-param 配置介绍


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


		<!-- 需要被初始化加载的容器配制文件 -->
		<context-param>
            <description> spring-context </description>
            <param-name> contextConfigLocation </param-name>
            <param-value> /WEB-INF/spring-root.xml </param-value>
		</context-param>

	</web-app>



**[web.xml文件范例](./webxml)中有如下一段描述：**


    <!--
    The context-param element contains the declaration of a web
    application's servlet context initialization parameters.

    Used in: web-app
    -->
    <!ELEMENT context-param (param-name, param-value, description?)>


**\<context-param>元素是我们常用的配置元素**

\<context-param>元素在\<web-app>元素节点下使用，此元素节点下必须有\<param-name>,\<param-value>两元素

\<description>元素是可选的

如果不配置\<context-param>元素，默认会去/WEB-INF/下加载applicationContext.xml文件


如果使用spring框架，这里\<param-name>已经在spring里定义了contextConfigLocation这个名字


至于\<param-value>的值，填写你的需要被加载的文件的路径





***

本篇所属：[java web篇](./Java/web/Index)

上一篇：[web.xml简介【4】之distributable介绍](./webxml-distributable-4)

下一篇：[web.xml简介【6】之filter介绍](./webxml-filter-6)