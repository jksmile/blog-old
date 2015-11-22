
#web.xml 简介【2】

## display-name 配置介绍


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

	</web-app>



**[web.xml文件范例](./webxml)中有如下一段描述：**


    <!--
    The display-name element contains a short name that is intended to be
    displayed by tools.  The display name need not be unique.

    Used in: filter, security-constraint, servlet, web-app

    Example:

    <display-name>Employee Self Service</display-name>
    -->
    <!ELEMENT display-name (#PCDATA)>


\<display-name>元素表示一个应用的名称

它可以在\<filter>,\<security-constraint>,\<servlet>,\<web-app>元素节点下使用。

***

本篇所属：[java web篇](./Java/web/Index)

上一篇：[web.xml 简介【1】之icon介绍](./webxml-icon)

下一篇：[web.xml简介【3】之description介绍](./webxml-description)