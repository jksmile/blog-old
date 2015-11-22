
#web.xml 简介【3】

## description 配置介绍


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

	</web-app>



**[web.xml文件范例](./webxml)中有如下一段描述：**


    <!--
    The description element is used to provide text describing the parent
    element.  The description element should include any information that
    the web application war file producer wants to provide to the consumer of
    the web application war file (i.e., to the Deployer). Typically, the tools
    used by the web application war file consumer will display the description
    when processing the parent element that contains the description.

    Used in: auth-constraint, context-param, ejb-local-ref, ejb-ref,
    env-entry, filter, init-param, resource-env-ref, resource-ref, run-as,
    security-role, security-role-ref, servlet, user-data-constraint,
    web-app, web-resource-collection
    -->
    <!ELEMENT description (#PCDATA)>


\<description>元素用来描述其所在父元素的信息

它可以在\<auth-constraint>,\<context-param>,\<ejb-local-ref>,\<ejb-ref>，\<env-entry>,\<filter>

,\<init-param>,\<resource-env-ref>,\<resource-ref>,\<run-as>,\<security-role>,\<security-role-ref>

\<servlet>,\<user-data-constraint>,\<web-app>,\<web-resource-collection>元素节点下使用。

***

本篇所属：[java web篇](./Java/web/Index)

上一篇：[web.xml 简介【2】之diplay-name介绍](./webxml-display-name)

下一篇：[web.xml简介【4】之distributable介绍](./webxml-distributable)